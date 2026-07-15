# ADR-0001: Plattform-Architektur — Git-basierte Inhalte mit schlanker Anwendungsschicht

**Status:** **Accepted** (bestätigt durch den Auftraggeber am 2026-07-15)
**Datum:** 2026-07-14 (vorgeschlagen) · 2026-07-15 (angenommen)
**Entscheider:** Auftraggeber (VersicherungsTech Magazin) auf Empfehlung
der Entwicklung
**Referenzen:** `docs/architecture-options.md` (vollständige Bewertung),
`docs/architecture-recommendation.md` (Zuschnitt),
`docs/product-requirements.md`, `docs/mvp-scope.md`

## Kontext

Für den MVP der VersicherungsTech KI-Akademie muss die grundlegende
technische Architektur festgelegt werden. Die prägenden Anforderungen:

- Der redaktionelle Review-Workflow ist bereits als Git-basiert entschieden
  (E5): Fach- und Regulatorik-Reviews laufen über Pull Requests, mit
  technisch erzwungenen Publikations-Gates (FR-14, AC-16), u. a. Blockade
  bei `QUELLE ZU VERIFIZIEREN` und fehlendem Regulatorik-Review.
- Alle Lernformate (Lektionen, Quiz, verzweigte Simulationen, Datenampel,
  Prompt-Bausatz) müssen deklarativ als Daten vorliegen (NFR-E1) und im
  Build validiert werden (NFR-E4); das Content-Modell darf keine
  Video-/Audio-Typen kennen (Produktvorgabe).
- Rechtsstand-Nachweis und Versionshistorie je Inhalt sind Pflicht (FR-13);
  regulatorische Inhalte müssen schnell und nachvollziehbar aktualisierbar
  sein (D6).
- Personenbezogene Daten sind auf ein Minimal-Datenmodell begrenzt
  (Konto, optionale Rolle, Einheiten-Status, Ergebnisse, Premium-Flag —
  AC-20.1); EU-Hosting mit AV-Verträgen (T5); kein Tracking ohne
  Rechtsgrundlage.
- Freemium ohne Bezahlstrecke im MVP (E2a, manuelles Premium-Flag);
  spätere Ausbaustufen: Zahlungsanbieter, Live-LLM-Übungen, B2B/SSO,
  Mehrsprachigkeit — dürfen nicht verbaut werden.
- Barrierefreiheit (WCAG 2.1 AA-Orientierung) und mobile Nutzung sind
  Abnahmekriterien (AC-18/19) und erfordern volle Kontrolle über das
  gerenderte HTML.
- Das Repository ist im Ausgangszustand (nur Dokumentation) — keine
  Altlasten.

Drei Varianten wurden bewertet (`docs/architecture-options.md`):
**A** Git-basierte Inhalte (Markdown/MDX + Strukturdaten),
**B** Headless CMS mit separatem Frontend,
**C** LMS/Standardsystem mit individueller Oberfläche.

## Entscheidung

Wir wählen **Variante A**: Git-basierte Inhalte mit einer schlanken,
selbst entwickelten Anwendungsschicht.

Konkret:

1. **Inhalte als Dateien im Repository:** Lektionen als Markdown/MDX mit
   Frontmatter-Metadaten (Status, Version, Rechtsstand, Quellen,
   Rollen-Tags); interaktive Formate als schemavalidierte Strukturdaten
   (YAML/JSON). Sprachschlüssel in der Dateikonvention von Beginn an
   (`de/` im MVP).
2. **Statische Generierung der Inhalte** durch ein Web-Framework mit
   Server-Anteilen (konkrete Framework-Wahl: ADR-0002); interaktive
   Übungen als wiederverwendbare, barrierefreie Komponenten, die die
   deklarativen Daten interpretieren.
3. **Schlanke Anwendungsschicht + PostgreSQL** für das
   Minimal-Nutzerdatenmodell (Auth, Fortschritt, Assessment-Ergebnis,
   Prüfung, Premium-Flag, Zertifikatsdatensatz). Premium-Volltexte werden
   nur nach serverseitiger Berechtigungsprüfung ausgeliefert.
4. **CI/CD als Durchsetzungsinstanz:** Schema-Validierung, Marker- und
   Status-Gates, Secret-Scan, Tests, a11y-Checks, Suchindex-Build (nur
   Status `Veröffentlicht`); Deployment ausschließlich nach ausdrücklicher
   Freigabe.
5. **EU-Hosting** für App, Datenbank und E-Mail-Versand (Anbieterwahl mit
   AV-Verträgen: Folgeentscheidung, siehe unten).
6. **Suche** aus dem Content-Build gespeist (Technik: ADR-0004).

## Betrachtete Alternativen

### Variante B — Headless CMS mit separatem Frontend
**Abgelehnt für den MVP**, weil: doppelter Systemaufbau (CMS + Frontend)
ohne Gegenwert — die CMS-Kernstärke (Redaktions-UI für nicht-technische
Teams) wird im MVP nicht benötigt (E5 entschied bewusst Git-Workflow);
verzweigte Simulationsstrukturen sind in CMS-Feldmodellen schlecht
abbild- und reviewbar; die erzwungenen Publikations-Gates und die
Rechtsstand-Historie müssten in CMS-Workflows nachgebaut werden; laufende
Kosten und (bei SaaS) Anbieter-/Drittlandprüfung zusätzlich.
**Wiedervorlage:** Falls das Redaktionsteam deutlich wächst, ist der
vorgesehene Weg jedoch nicht B, sondern eine Git-basierte Editor-UI
(z. B. Sveltia/Decap) über dem bestehenden Content — ohne
Architekturwechsel.

### Variante C — LMS/Standardsystem (z. B. Moodle)
**Abgelehnt**, weil: Datenhaltung widerspricht der Datensparsamkeit
(LMS erfassen standardmäßig umfangreiche Aktivitätsdaten — Konflikt mit
FR-10.5/US-10.1); Inhalte in der LMS-Datenbank ohne brauchbare
Versionierung/Diffs (Konflikt mit FR-13/NFR-E3); die drei projektprägenden
Übungsformate wären Plugin-Entwicklung gegen ein Fremdsystem mit
unsicherer a11y-/Mobile-Qualität; hoher Lock-in; UI-Bruch zur
Magazin-Anmutung. Der einzige klare Vorteil (fertige Zertifikats-/
Kurslogik) wiegt die Nachteile nicht auf, da diese Bausteine klein sind.

## Konsequenzen

### Positiv
- Review-Gates, Versionierung, Rechtsstand-Historie und „nur
  Veröffentlichtes ist sichtbar“ sind Struktureigenschaften statt
  Eigenentwicklung gegen ein Fremdsystem.
- Genau ein System hält personenbezogene Daten; Datenschutz by Design
  wird überprüfbar einfach (Threat Model T20: Schadensbegrenzung).
- Minimale laufende Kosten; freie EU-Hosterwahl; keine Lizenz-/
  SaaS-Abhängigkeit; Inhalte in offenen, portablen Formaten.
- Volle Kontrolle über HTML/Interaktion → a11y- und Mobile-Abnahme
  (AC-18/19) erreichbar.
- Ausbaustufen andocken statt umbauen: Zahlungsanbieter setzt das
  Premium-Flag per Webhook; SSO als zusätzlicher Anmeldeweg; Editor-UI
  über Git; Mehrsprachigkeit über Dateikonvention.

### Negativ / Kosten
- Redaktion arbeitet in Git (Markdown/YAML + PR) — erfordert Einarbeitung
  und ein Autoren-Handbuch; für nicht-technische Gelegenheitsautoren eine
  Hürde (bewusst akzeptiert mit E5).
- Konto-, Fortschritts-, Prüfungs- und Zertifikatslogik sind
  Eigenentwicklung — inkl. Verantwortung für deren Sicherheit
  (Threat Model T1–T10) und Betrieb (Backups, Updates).
- Kein fertiges Kurs-Ökosystem: jedes neue Übungsformat ist
  Schema + Komponente (dafür exakt passend und wiederverwendbar).

### Risiken und Gegensteuerung
- *Schema-Design wird zum Engpass:* Content-Schemata als erste
  Implementierungsaufgabe mit eigener Entscheidung (ADR-0003), an einer
  Musterlektion je Format validiert, bevor Kursproduktion startet.
- *Eigenentwicklung unterschätzt:* Reduktionspfad in `docs/mvp-scope.md`
  §3 ist vereinbart; Minimal-Datenmodell begrenzt die Komplexität.

## Bestätigung durch den Auftraggeber (2026-07-15)

Der Auftraggeber hat am 2026-07-15 entschieden:

> Wir wählen Variante A: Git-basierte Inhalte mit einer schlanken
> individuellen Anwendungsschicht und PostgreSQL für das minimale
> Nutzerdatenmodell.

### Mit der Bestätigung verbundene Konsequenzen

- Die Grundsatz-Architektur ist verbindlich; Abweichungen erfordern ein
  neues ADR mit Begründung.
- Die Folgeentscheidungen (ADR-0002 Framework/Hosting, ADR-0003
  Content-Schemata, ADR-0004 Suchtechnik) werden auf dieser Basis
  erarbeitet; die Suchtechnik wird erst **nach** Definition der
  Content-Schemata entschieden (Vorgabe des Auftraggebers).
- Das Nutzerdatenmodell muss über das Minimalprinzip hinaus die
  Lebenszyklen **Löschung, Anonymisierung, Deaktivierung und
  Zertifikats-Widerruf** technisch unterstützen (Vorgabe des Auftraggebers
  aus dem vorläufigen Löschkonzept, siehe
  `docs/security-and-privacy-rules.md` §5).
- Mehrsprachigkeit wird technisch vorbereitet (Sprachschlüssel in der
  Dateikonvention); MVP-Sprache ist ausschließlich Deutsch.
- Premium-Zugang wird als Berechtigungs-Flag umgesetzt (bestätigt).

### Bewusst akzeptierte Nachteile

Der Auftraggeber akzeptiert mit dieser Entscheidung ausdrücklich:

1. **Redaktionsarbeit in Git:** Autorinnen und Reviewer arbeiten mit
   Markdown/YAML und Pull Requests; es gibt im MVP keine grafische
   Redaktionsoberfläche. Abmilderung: Autoren-Handbuch, Vorlagen,
   PR-Vorschau; Git-basierte Editor-UI als mögliche Ausbaustufe.
2. **Eigenverantwortung für die Anwendungsschicht:** Konto-, Fortschritts-,
   Prüfungs- und Zertifikatslogik inkl. deren Sicherheit
   (Threat Model T1–T10) und Betrieb (Backups, Updates) sind
   Eigenentwicklung ohne Hersteller-Support.
3. **Kein fertiges Kurs-Ökosystem:** Jedes neue Übungsformat erfordert
   Schema- und Komponentenarbeit; es gibt keine Plugin-Landschaft wie bei
   einem LMS.
4. **Übersetzungs-Workflows bleiben manuell**, bis eine
   Mehrsprachigkeits-Ausbaustufe entschieden ist.

## Folgeentscheidungen (nicht Teil dieses ADR)

| # | Gegenstand | Format |
|---|---|---|
| ADR-0002 | Web-Framework und Hosting-Anbieter (EU, AV-Verträge) | ADR + Anbieterprüfung |
| ADR-0003 | Content-Schemata (Lektion, Quiz, Simulation, Ampel, Prompt-Vorlage) | ADR + Schemadateien |
| ADR-0004 | Suchtechnik (Build-Index vs. selbst gehostete Suchmaschine) | ADR |
| — | E-Mail-Anbieter (EU), Backup-/DB-Betrieb | Anbieterprüfung (V3) |
