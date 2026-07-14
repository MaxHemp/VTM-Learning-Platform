# Architekturempfehlung — VersicherungsTech KI-Akademie (MVP)

**Status:** Empfehlung zur Bestätigung durch den Auftraggeber
**Stand:** 2026-07-14
**Grundlagen:** `docs/architecture-options.md` ·
**Formale Entscheidung:** `docs/adr/0001-platform-architecture.md`

---

## 1. Empfehlung

**Variante A: Git-basierte Inhalte (Markdown/MDX + deklarative
Strukturdaten) mit einer schlanken eigenen Anwendungsschicht für
Nutzerdaten.**

## 2. Begründung in fünf Punkten

1. **Die wichtigste Architekturentscheidung ist bereits gefallen.** Mit E5
   (Git-basierter Redaktions-Workflow, keine Redaktions-UI im MVP) ist der
   Kern von Variante A beschlossen. Ein Headless CMS (B) würde diesen
   Workflow durch einen zweiten, parallelen ersetzen oder nachbauen; ein
   LMS (C) würde ihm widersprechen.
2. **Die harten Pflichten fallen strukturell ab, statt gebaut zu werden.**
   Erzwungene Review-Gates (AC-16), Rechtsstand-Historie (FR-13),
   reproduzierbare Veröffentlichungen (NFR-E3) und „nur Veröffentlichtes
   ist auffindbar“ (AC-17.4) sind in Git + CI + statischem Build
   Grundeigenschaften — in B und C sind sie Custom-Entwicklung gegen ein
   Fremdsystem.
3. **Datenschutz by Design wird einfach statt mühsam.** Es gibt genau ein
   System mit personenbezogenen Daten (die eigene kleine Datenbank mit dem
   Minimal-Datenmodell aus AC-20.1). Inhalte sind reine Textdateien ohne
   Personenbezug. Kein CMS-/LMS-System sammelt nebenbei Daten, die wir laut
   eigenen Regeln gar nicht haben wollen.
4. **Die projektprägenden Lernformate brauchen eigene Komponenten — in
   jeder Variante.** Verzweigte Fallsimulationen, Datenampel und
   Prompt-Bausatz mit voller Barrierefreiheit existieren nirgends von der
   Stange. Wenn das Frontend ohnehin Eigenentwicklung ist, liefert A den
   kürzesten Weg: deklarative Formate im Repo → Schema-Validierung im
   Build → Komponente rendert.
5. **Geringste Kosten, geringste Abhängigkeit, videofreier Vorteil
   ausgespielt.** Ohne Video braucht es keine Media-Pipeline — Inhalte sind
   klein, statisch auslieferbar, günstig zu hosten (EU-Hoster frei wählbar)
   und schnell auf Mobilgeräten (NFR-B/C). Kein Lizenz- oder SaaS-Lock-in.

## 3. Zuschnitt der empfohlenen Architektur

```
┌────────────────────────── Git-Repository ──────────────────────────┐
│  content/            docs/               app/                      │
│  ├─ kurse/…           (Regeln, ADRs)      (Web-App + Übungs-       │
│  ├─ lektionen (MDX)                        Komponenten + API)      │
│  ├─ quiz|simulation|ampel|prompts (YAML/JSON, schemavalidiert)     │
│  └─ quellen/metadaten (Frontmatter: Status, Version, Rechtsstand)  │
└──────────────┬─────────────────────────────────────────────────────┘
               │  Pull Request = Fach-/Regulatorik-Review (FR-14)
               ▼
        CI/CD-Pipeline
        ├─ Schema- & Marker-Gates (blockiert QUELLE ZU VERIFIZIEREN,
        │  Regulatorik ohne Review-Nachweis, Video-Typen, fehlende DoD-Felder)
        ├─ Tests, a11y-Checks, Suchindex-Build
        └─ Deployment NUR nach ausdrücklicher Freigabe
               │
               ▼
┌─────────────────────── EU-Hosting ─────────────────────────────────┐
│  Statisch generierte Inhalte (CDN-/cachefähig)                     │
│  + App-Server (Konto, Fortschritt, Prüfung, Premium-Flag,          │
│    Zertifikat-PDF, Verifikationsseite)                             │
│  + PostgreSQL (Minimal-Datenmodell, AC-20.1)                       │
│  + Suchindex (Build-Zeit; nur veröffentlichte Inhalte)             │
│  + Transaktions-E-Mail (Verifizierung, Passwort-Reset; EU-Anbieter)│
└────────────────────────────────────────────────────────────────────┘
```

Details zu Datenflüssen: `docs/data-flow-overview.md`.

### Leitplanken

- **Content-Schemata zuerst:** Vor der ersten Lektion werden die
  deklarativen Formate (Lektion, Quiz, Simulation, Ampel, Prompt-Vorlage)
  als Schemata definiert und validiert — sie sind der eigentliche Kern der
  Plattform (Folge-ADR 0002/0003).
- **Premium = ein Flag, kein Framework:** Freemium wird als simples
  Berechtigungs-Flag am Konto umgesetzt (E2a); der spätere Zahlungsanbieter
  (Ausbaustufe 1) setzt dieses Flag per Webhook — kein Umbau nötig.
- **Auth von Anfang an austauschbar:** Session-basierte E-Mail/Passwort-
  Anmeldung hinter einer schmalen Schnittstelle, sodass SSO/OIDC
  (Ausbaustufe 3) als zusätzlicher Anmeldeweg andocken kann, ohne das
  Nutzerdatenmodell zu ändern.
- **Magazin-Integration über Design und Verlinkung:** Subdomain (z. B.
  `akademie.versicherungstech-magazin.de` — zu bestätigen), gemeinsame
  Design-Anmutung; technische Kopplung an die Magazin-Website bewusst lose
  halten, bis deren Technik bekannt ist (offene Frage T8).
- **Mehrsprachigkeit nicht verbauen:** Dateikonvention mit Sprachschlüssel
  von Anfang an (`de/` als einzige Sprache im MVP).

## 4. Ehrliche Schwächen der Empfehlung und ihre Behandlung

| Schwäche | Behandlung |
|---|---|
| Redaktion braucht Git-Grundkenntnisse | Autoren-Handbuch + Vorlagen je Format; PR-Vorschau-Deployments zum Gegenlesen; bei Teamwachstum: Git-basierte Editor-UI (z. B. Sveltia/Decap) als dünne Schicht — Architektur bleibt unverändert (Ausbaustufe 4) |
| Alles Nutzerseitige ist Eigenentwicklung | Umfang ist klein und klar begrenzt (Minimal-Datenmodell); Reduktionspfad in `docs/mvp-scope.md` §3 greift bei Druck |
| Kein fertiges Zertifikatsmodul (wie im LMS) | PDF-Erzeugung + Verifikationsseite sind wenige, gut testbare Bausteine (FR-12, AC-14) |
| Übersetzungs-Workflows später manuell | Erst relevant ab Mehrsprachigkeits-Ausbaustufe; Dateikonvention hält den Weg offen |

## 5. Was diese Empfehlung NICHT festlegt (Folgeentscheidungen)

| # | Offen | Geplantes Format |
|---|---|---|
| F1 | Konkretes Web-Framework (z. B. Next.js vs. Astro) und Hosting-Anbieter (EU) | ADR-0002 + Anbieterprüfung inkl. AV-Vertrag (T5, V3) |
| F2 | Content-Schemata im Detail (Lektion, Quiz, Simulation, Ampel, Prompt) | ADR-0003 + Schema-Dateien |
| F3 | Suchtechnik (Build-Index vs. Meilisearch) | ADR-0004, abhängig von F1 |
| F4 | Transaktions-E-Mail-Anbieter (EU, AV-Vertrag) | Anbieterprüfung |
| F5 | Datenbank-/Backup-Betrieb (Managed vs. selbst) | Teil von F1/Hosting |

Alle Punkte sind vor Implementierungsstart zu entscheiden
(**ENTSCHEIDUNG AUFTRAGGEBER** bzw. Vorschlag durch Entwicklung mit
Freigabe); sie ändern die Grundsatzentscheidung dieses Dokuments nicht.
