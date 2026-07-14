# Architekturvarianten — VersicherungsTech KI-Akademie (MVP)

**Status:** Entwurf zur Entscheidung durch den Auftraggeber
**Stand:** 2026-07-14
**Grundlagen:** `docs/product-requirements.md`, `docs/mvp-scope.md`,
`docs/acceptance-criteria.md`, `docs/security-and-privacy-rules.md`,
`docs/definition-of-done.md`
**Empfehlung:** `docs/architecture-recommendation.md` ·
**Entscheidung:** `docs/adr/0001-platform-architecture.md`

---

## 1. Architekturprägende Anforderungen (Analyse-Ergebnis)

Aus den vorhandenen Dokumenten ergeben sich folgende Anforderungen, die die
Architekturwahl dominieren:

1. **Git-basierter Review-Workflow ist bereits entschieden (E5):**
   Statuswechsel, Fach- und Regulatorik-Review laufen über
   Pull Requests; erzwungene Publikations-Gates (Regulatorik-Marker,
   `QUELLE ZU VERIFIZIEREN` blockiert Veröffentlichung) müssen technisch
   durchgesetzt werden (FR-14, AC-16).
2. **Deklaratives Content-Modell:** Quiz, verzweigte Simulationen,
   Datenampel und Prompt-Bausatz sind Daten, kein Code (NFR-E1, FR-6.4,
   FR-7.6, FR-8.4). Neue Übungen ohne Code-Änderung (AC-9.6).
3. **Automatisierte Content-Prüfungen im Build:** Pflichtfelder, Marker-
   Konsistenz, Blockade verbotener Inhaltstypen — inkl. „kein Video-Typ im
   Content-Modell“ (NFR-E4, AC-7.5, AC-15.2).
4. **Wenig personenbezogene Daten, klar abgegrenzt:** Konto, Rolle
   (optional), Einheiten-Status, Modul-/Prüfungsergebnisse, Premium-Flag —
   mehr nicht (FR-10.5, FR-16, AC-20.1). Der gesamte Lerninhalt selbst ist
   **nicht personenbezogen** und öffentlich bzw. premium-gated.
5. **Freemium ohne Bezahlstrecke im MVP (E2a):** Premium ist ein manuell
   gesetztes Konto-Flag; Zahlungsanbieter kommt später (Ausbaustufe 1) —
   die Architektur muss das Nachrüsten erlauben, nicht vorwegnehmen.
6. **EU-/DACH-Hosting-Präferenz, AV-Verträge** (T5, NFR-D1); Datenschutz by
   Design; kein Tracking ohne Rechtsgrundlage (NFR-D3).
7. **Barrierefreiheit und mobile Nutzung** als Abnahmekriterien (AC-18/19) —
   die Architektur muss volle Kontrolle über das ausgelieferte HTML geben.
8. **Suche als Kernfeature** über alle veröffentlichten Inhalte (FR-15, R10).
9. **Kein Video** — keine Media-Pipeline, kein Streaming, keine großen
   Assets: Inhalte sind Text + Strukturdaten. Das reduziert die
   Anforderungen an CMS/LMS erheblich.
10. **Rechtsstand-Updates müssen schnell und nachvollziehbar sein** (D6,
    FR-13): Änderung → Review → Veröffentlichung in kurzer Zeit, mit
    Versionshistorie.
11. **Repository-Zustand:** Reines Dokumentations-Repository, keine
    Altlasten — alle Varianten starten auf der grünen Wiese; das
    Content-als-Dateien-Muster (`docs/`, geplant `content/`) ist bereits
    angelegt (`CLAUDE.md` Abschnitt 6).
12. **Ausbaustufen:** Bezahlmodell (Stufe 1), Live-LLM (Stufe 2),
    B2B/SSO (Stufe 3), Mehrsprachigkeit (explizit nicht MVP, A4) — die
    Architektur soll diese Stufen nicht verbauen.

Gemeinsame Konsequenz für alle Varianten: Es braucht in jedem Fall eine
**kleine eigene Anwendungsschicht** für Konten, Lernfortschritt, Prüfung,
Premium-Flag und Zertifikats-PDF — kein CMS und kein statischer Generator
deckt das datensparsam ab. Die Varianten unterscheiden sich also primär in
der **Content-Haltung und -Pflege**, nicht in der Nutzerdatenhaltung.

## 2. Die drei Varianten

### Variante A — Git-basierte Inhalte (Markdown/MDX + Strukturdaten)

**Aufbau:**

- Inhalte liegen als Dateien im Repository: Lektionen als Markdown/MDX mit
  Frontmatter-Metadaten (Version, Status, Rollen-Tags, Rechtsstand,
  Quellen); interaktive Formate (Quiz, Simulation, Datenampel,
  Prompt-Bausatz) als strukturierte Daten (YAML/JSON) mit Schema.
- Ein Web-Framework mit statischer Generierung + Server-Anteilen (z. B.
  Next.js oder Astro — konkrete Wahl in ADR-0002) rendert Inhalte zur
  Build-Zeit; interaktive Übungen sind wiederverwendbare Komponenten, die
  die deklarativen Daten interpretieren.
- Kleine Anwendungsschicht (gleiche Codebasis oder schlanker Dienst) +
  relationale Datenbank (z. B. PostgreSQL) für Konto, Fortschritt, Prüfung,
  Premium-Flag.
- CI/CD erzwingt die Content-Gates: Schema-Validierung, Marker-Logik,
  Status-Regeln; Veröffentlichung = Merge auf den Hauptbranch + Deployment
  nach Freigabe.
- Suche über Build-Zeit-Index (z. B. Pagefind) oder selbst gehostete
  Suchmaschine (z. B. Meilisearch), gespeist aus dem Content-Build.

**Charakter:** „Content as Code“ — Redaktion arbeitet in Git (PR-Review =
FR-14), Plattform ist ein maßgeschneidertes, schlankes Produkt.

### Variante B — Headless CMS mit separatem Frontend

**Aufbau:**

- Inhalte liegen in einem Headless CMS (self-hosted EU, z. B. Directus/
  Payload, oder EU-SaaS, z. B. Storyblok) und werden über dessen API vom
  Frontend abgerufen bzw. zur Build-Zeit gezogen.
- Frontend wie in A (eigenes Web-Framework, eigene Übungskomponenten).
- Anwendungsschicht + DB für Nutzerdaten wie in A (das CMS hält **keine**
  personenbezogenen Lernendendaten).
- Redaktions-UI, Rollen/Rechte und Draft/Publish kommen aus dem CMS;
  die projektspezifischen Gates (Regulatorik-Review-Zwang,
  `QUELLE ZU VERIFIZIEREN`-Blockade) müssen in CMS-Workflows nachgebaut
  oder per Custom-Hook ergänzt werden.

**Charakter:** komfortable Redaktionsoberfläche, dafür zwei Systeme
(CMS + Frontend) mit Modellierungs- und Abstimmungsaufwand.

### Variante C — LMS/Standardsystem mit individueller Oberfläche

**Aufbau:**

- Ein etabliertes Lernmanagementsystem (realistisch: Moodle als
  Open-Source-Standard, self-hosted EU; alternativ Open edX oder ein
  kommerzielles DACH-LMS) liefert Kurse, Quiz, Fortschritt, Prüfungen und
  Zertifikate als Standardfunktionen.
- Individualisierung über Theme/Plugins; die projektspezifischen Formate
  (verzweigte Fallsimulationen, Datenampel, Prompt-Bausatz) über
  Plugin-Entwicklung oder Autorentools wie H5P (Branching Scenario —
  textbasiert nutzbar, aber auf Medieninhalte ausgelegt).
- Freemium/Landingpage entweder im LMS nachgebaut oder als vorgelagerte
  eigene Website mit Übergabe ins LMS.

**Charakter:** viel Standardfunktionalität sofort, dafür Anpassung gegen
das System statt mit ihm; das Produkterlebnis wird vom LMS-Paradigma
geprägt.

## 3. Bewertung

Skala: **++** sehr gut / **+** gut / **o** neutral bzw. mit Aufwand lösbar /
**−** schwach / **−−** kritisch. Bewertung bezogen auf **dieses Projekt**
(nicht allgemein).

| Kriterium | A: Git-basiert | B: Headless CMS | C: LMS |
|---|:---:|:---:|:---:|
| Entwicklungsaufwand (MVP) | o | o/− | o |
| Laufende Kosten | ++ | o | o |
| Redaktionelle Bedienbarkeit | o | ++ | + |
| Versionierbarkeit | ++ | o | − |
| Skalierbarkeit | + | + | + |
| Datenschutz / Datensparsamkeit | ++ | + | − |
| EU-/DACH-Hosting | ++ | + | + |
| Mehrsprachigkeit (Ausbaustufe) | + | ++ | ++ |
| Interaktivität (eigene Formate) | ++ | + | − |
| Zertifikate | + | + | ++ |
| Suchfunktion | + | + | o |
| Aktualisierung regulatorischer Inhalte | ++ | + | − |
| Herstellerabhängigkeit | ++ | o | − |
| Integration Magazin-Website | + | + | − |
| Eignung für schnellen MVP | + | o | o |

### Begründungen je Kriterium

**Entwicklungsaufwand:**
- **A (o):** Alles Nutzerseitige (Konto, Fortschritt, Prüfung, Übungs-
  Komponenten) ist Eigenentwicklung — aber genau diese Teile sind in allen
  Varianten Eigenentwicklung. A spart die CMS-/LMS-Integration und hat den
  geringsten Abstimmungsaufwand zwischen Systemen. Umfang bleibt durch den
  Reduktionspfad (`docs/mvp-scope.md` §3) steuerbar.
- **B (o/−):** Frontend-Aufwand wie A **plus** CMS-Aufbau, Content-
  Modellierung im CMS (verzweigte Simulationen in CMS-Feldstrukturen sind
  mühsam) und Nachbau der Review-Gates in CMS-Workflows.
- **C (o):** Standardfunktionen (Kurs, Quiz, Zertifikat) sofort da; aber
  Freemium-Logik, Datenampel, Prompt-Werkstatt, verzweigte Simulationen in
  der geforderten Qualität sowie das geforderte UI-/a11y-Niveau bedeuten
  Plugin- und Theme-Entwicklung gegen ein großes Fremdsystem — erfahrungs-
  gemäß kein echter Aufwandsvorteil, sobald man das Standard-Erlebnis
  verlässt.

**Laufende Kosten:**
- **A (++):** Statisch ausgelieferte Inhalte + kleiner App-Server + kleine
  DB; kein Lizenz-/SaaS-Abo. Geringste Grundlast.
- **B (o):** Zusätzlich CMS-Betrieb (Self-hosted: Wartung/Updates) oder
  SaaS-Abo (laufende Kosten, steigen mit Nutzern/Einträgen).
- **C (o):** LMS-Hosting mit größerem Ressourcenbedarf, laufende
  Sicherheitsupdates eines großen PHP-/Python-Systems, ggf. Plugin-Pflege
  bei jedem Major-Update.

**Redaktionelle Bedienbarkeit:**
- **A (o):** Redaktion arbeitet mit Markdown/YAML in Git — für ein kleines,
  eingearbeitetes Team gut machbar (E5 wurde genau so entschieden);
  Web-Editieroberflächen auf Git-Basis (z. B. Sveltia/Decap CMS) können
  später als dünne Schicht ergänzt werden, ohne die Architektur zu ändern.
  Für nicht-technische Gelegenheitsautoren bleibt es eine Hürde —
  ehrlichster Schwachpunkt von A.
- **B (++):** Beste Autorenerfahrung (WYSIWYG-Formulare, Vorschau,
  Medienverwaltung — Letzteres hier kaum nötig, da kein Video/Bildfokus).
- **C (+):** Vorhandene Autorenwerkzeuge, aber LMS-Redaktionsoberflächen
  sind notorisch verschachtelt; eigene Formate brauchen eigene Editoren.

**Versionierbarkeit:**
- **A (++):** Git ist das Versionssystem: jede Änderung diffbar,
  Rechtsstand-Historie vollständig, Veröffentlichungen reproduzierbar
  (NFR-E3 nativ erfüllt), Rollback trivial.
- **B (o):** CMS-Versionierung existiert, ist aber gröber (Eintrags-
  Snapshots), Diff-Qualität und Audit-Tiefe anbieterabhängig; „Stand der
  gesamten Plattform zum Zeitpunkt X“ ist schwer reproduzierbar.
- **C (−):** Inhalte leben in der LMS-Datenbank; Versionierung rudimentär,
  Diffs praktisch nicht vorhanden — für den Rechtsstand-Nachweis (FR-13)
  ein echtes Problem.

**Skalierbarkeit:** Alle drei tragen die realistischen Nutzerzahlen einer
Fach-Lernplattform problemlos (+). A liefert Inhalte statisch/cachebar aus
(sehr günstig skalierend); B ähnlich mit Build-Zeit-Abruf; C skaliert
bewährt, aber ressourcenhungriger.

**Datenschutz / Datensparsamkeit:**
- **A (++):** Ein einziges selbst kontrolliertes Datenhaltungssystem mit
  exakt dem definierten Minimal-Datenmodell (AC-20.1); Inhalte enthalten
  keine personenbezogenen Daten; kein Drittanbieter im Kernpfad.
- **B (+):** Nutzerdaten wie A; aber ein zusätzliches System mit eigenen
  Konten (Redaktion), bei SaaS zusätzlich AV-Vertrag/Drittlandprüfung.
- **C (−):** LMS speichern by Design viel (Logs, Aktivitätsdaten,
  Forenreste, detaillierte Klickpfade) — Datensparsamkeit muss gegen die
  Standardkonfiguration erkämpft und bei jedem Update verteidigt werden;
  Konflikt mit FR-10.5/US-10.1.

**EU-/DACH-Hosting:**
- **A (++):** Freie Wahl jedes EU-Hosters (auch klassisches deutsches
  Hosting), minimale Anforderungen.
- **B (+):** Self-hosted im EU-Rechenzentrum gut machbar; EU-SaaS verfügbar
  (AV-Vertrag prüfen).
- **C (+):** Self-hosted EU üblich; DACH-Moodle-Hoster existieren.

**Mehrsprachigkeit (Ausbaustufe, nicht MVP — A4):**
- **A (+):** Über Verzeichnis-/Dateikonvention sauber machbar, aber
  Übersetzungs-Workflow ist Handarbeit bzw. spätere Tool-Anbindung.
- **B (++):** i18n ist CMS-Kernfunktion inkl. Übersetzungs-Workflows.
- **C (++):** LMS sind vielsprachig gebaut (UI + Inhalte).

**Interaktivität (verzweigte Simulationen, Datenampel, Prompt-Bausatz):**
- **A (++):** Eigene Komponenten interpretieren eigene deklarative Formate —
  exakt die geforderte Didaktik, volle a11y-Kontrolle (AC-9/10/11/18),
  Schema-Validierung im Build.
- **B (+):** Gleiche Frontend-Komponenten möglich; aber die Formate müssen
  in CMS-Content-Strukturen modelliert und gepflegt werden — verzweigte
  Bäume in CMS-Relationen sind fehleranfällig und schlecht reviewbar.
- **C (−):** Standard-Quiz stark, aber die drei projektprägenden Formate
  erfordern Plugin-Entwicklung im LMS-Rahmen oder H5P-Kompromisse;
  Barrierefreiheit und mobile Qualität der Ergebnisse sind schwerer zu
  garantieren als bei eigenen Komponenten.

**Zertifikate:**
- **A/B (+):** PDF-Erzeugung + Verifikationsseite sind überschaubare
  Eigenentwicklung mit voller Gestaltungskontrolle (FR-12).
- **C (++):** Zertifikate und Badges sind LMS-Standardfunktionen —
  einziger klarer Funktionsvorsprung von C.

**Suchfunktion:**
- **A (+):** Build-Zeit-Index über alle veröffentlichten Inhalte ist
  einfach und präzise (nur Status `Veröffentlicht` wird gebaut → AC-17.4
  strukturell erfüllt); Facetten (Rolle/Typ) aus Frontmatter.
- **B (+):** Gleichwertig, gespeist aus der CMS-API.
- **C (o):** LMS-interne Suche ist erfahrungsgemäß schwach; gute Suche
  hieße auch hier ein zusätzlicher Suchdienst.

**Aktualisierung regulatorischer Inhalte:**
- **A (++):** Rechtsstand-Änderung = PR mit Diff, erzwungenem
  Regulatorik-Review (Branch-Protection + CI-Gate), sauberer Historie und
  sofortigem Rebuild — der in AC-15/16 geforderte Prozess fällt fast
  von selbst aus der Architektur.
- **B (+):** Schnell änderbar per UI; die erzwungenen Gates und die
  Nachvollziehbarkeit müssen im CMS nachgebaut werden.
- **C (−):** Änderungen in LMS-Datenbank ohne brauchbare Diffs; Review-Gates
  komplett custom; Rechtsstand-Nachweis mühsam.

**Herstellerabhängigkeit:**
- **A (++):** Inhalte sind portable Textdateien in offenen Formaten;
  Framework austauschbar; kein Anbieter im Kern.
- **B (o):** Content-Export möglich, aber Struktur/Workflows hängen am CMS;
  SaaS-Preismodelle können sich ändern.
- **C (−):** Inhalte, Didaktik-Umsetzung und Prozesse wachsen ins
  LMS-Paradigma hinein; Migration heraus ist teuer.

**Integration Magazin-Website:**
- **A/B (+):** Eigenes Frontend kann Design und Navigation des Magazins
  aufnehmen; Verlinkung/Subdomain unkompliziert. (Tiefere Integration hängt
  von der Magazin-Technik ab — unbekannt, siehe offene Frage T8.)
- **C (−):** LMS-UI bricht erfahrungsgemäß mit dem redaktionellen
  Erscheinungsbild; Nutzerführung Magazin → LMS wirkt wie ein Systemwechsel.

**Eignung für schnellen MVP:**
- **A (+):** Ein System, ein Deployment, kontrollierbarer Umfang; der
  bereits entschiedene Git-Review (E5) ist nativ enthalten statt
  nachgebaut.
- **B (o):** Zwei Systeme parallel aufbauen und verzahnen kostet die Zeit,
  die die Redaktions-UI spart — die im MVP (kleines Team, E5) gar nicht
  gefordert ist.
- **C (o):** Schneller Start mit Standardfunktionen, aber der Weg zum
  geforderten Produkterlebnis (Freemium, eigene Formate, a11y, mobiles
  Lesen, Magazin-Anmutung) führt durch zähe Anpassungsarbeit; hohes Risiko,
  dass der MVP „nach LMS“ statt nach VersicherungsTech aussieht (R9/R10).

## 4. Zusammenfassung

- **Variante A** gewinnt bei den Kriterien, die dieses Projekt prägen:
  Versionierung/Rechtsstand, erzwungene Review-Gates, Datensparsamkeit,
  eigene interaktive Formate, geringe Kosten, Unabhängigkeit. Ihr einziger
  struktureller Nachteil (Redaktions-UI) ist durch E5 explizit akzeptiert
  und später durch eine Git-basierte Editor-Schicht heilbar.
- **Variante B** ist die richtige Wahl, wenn ein größeres, nicht-technisches
  Redaktionsteam täglich Inhalte pflegt — das ist im MVP nicht die Lage und
  wurde mit E5 anders entschieden.
- **Variante C** spielt ihre Stärken (fertige Kurs-/Zertifikatslogik,
  Mehrsprachigkeit) in Szenarien aus, die hier nicht gefordert sind, und
  ist bei den kritischen Anforderungen (Datensparsamkeit, Versionierung,
  eigene Formate, Produkterlebnis) die schwächste Option.

**Empfehlung: Variante A** — Begründung und Zuschnitt in
`docs/architecture-recommendation.md`, formale Entscheidung in
`docs/adr/0001-platform-architecture.md`
(**ENTSCHEIDUNG AUFTRAGGEBER**).
