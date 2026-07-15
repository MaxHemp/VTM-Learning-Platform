# Offene Fragen und Entscheidungen — VersicherungsTech KI-Akademie

**Status:** lebendes Dokument
**Stand:** 2026-07-14

Dieses Dokument sammelt offene Entscheidungen, ungeklärte Fragen und
Annahmen, die validiert werden müssen. Erledigte Punkte werden mit
Entscheidung und Datum in den Abschnitt „Entschieden“ verschoben.

## 1. Produkt und Strategie

| # | Frage | Warum wichtig | Vorschlag / Stand |
|---|---|---|---|
| P1 | ~~Geschäftsmodell~~ | — | **Entschieden 2026-07-14:** Freemium-Abo (siehe unten) |
| P2 | ~~Startumfang / Pilot-Lernpfad~~ | — | **Entschieden 2026-07-14:** rollenunabhängiger Grundkurs „KI-Führerschein für den Versicherungsalltag“ |
| P3 | ~~IDD-Anrechnung~~ | — | **Entschieden 2026-07-14:** keine IDD-Anrechnung. Form des Nachweises (Badges/Zertifikat) siehe P7 |
| P6 | ~~Freemium-Grenze~~ | — | **Entschieden 2026-07-14:** Assessment + Modul 1 frei; Module 2–7, Prüfung, Zertifikat Premium (E1 bestätigt) |
| P7 | Nachweisform im MVP: nur Badges, nur PDF-Zertifikat, oder beides? | Aufwand Prüfungslogik und PDF-Erzeugung | Vorschlag: Badges je Modul + einfaches PDF-Zertifikat nach Abschlussprüfung — ENTSCHEIDUNG AUFTRAGGEBER |
| P8 | Preismodell des Premium-Abos (Preis, monatlich/jährlich, Zahlungsanbieter)? | Umsetzung Bezahlstrecke im MVP oder Nachlagerung | offen — ENTSCHEIDUNG AUFTRAGGEBER |
| P4 | Verhältnis zum VersicherungsTech Magazin: gemeinsame Accounts, Branding, Domain? | Login-Konzept, SEO, redaktionelle Workflows | offen |
| P5 | Erfolgskriterien und Messgrößen (KPIs) für die Plattform? | Ohne Zielwerte keine Priorisierung | Arbeitsfassung in `docs/project-vision.md`, Zielwerte offen |

## 2. Inhalte und Didaktik

| # | Frage | Warum wichtig | Vorschlag / Stand |
|---|---|---|---|
| D1 | Anrede „Sie“ oder „Du“? | Konsistenz aller Inhalte; Branchenkonvention vs. Lernplattform-Üblichkeit | `ANNAHME` derzeit: „Sie“ — zu bestätigen |
| D2 | Einheitslänge 10–20 Minuten realistisch? | Kernannahme der Didaktik | `ANNAHME` — mit Pilotnutzern validieren |
| D3 | Welche KI-Tools kommen auf die Freigabeliste für praktische Übungen? | Ohne Liste keine Tool-Übungen; Datenschutz- und Kostenfragen | offen; Kriterienkatalog nötig (Datenschutz, Verfügbarkeit DACH, Kosten, Stabilität) |
| D4 | Rollenübergreifende Basismodule: Zuschnitt und Pflichtstatus? | Vermeidet Redundanz in 10 Rollenpfaden | Vorschlag in `docs/didactic-principles.md`, Zuschnitt offen |
| D5 | Umgang mit CH/AT-Besonderheiten: eigene Varianten oder Kennzeichnung im Text? | Aufwand vs. Präzision (FINMA/FMA, revDSG vs. DSGVO) | `ANNAHME` derzeit: Kennzeichnung im Text, keine separaten Länderpfade |
| D6 | Aktualisierungszyklus für regulatorische Inhalte (z. B. AI-Act-Umsetzungsfristen)? | Rechtsstand veraltet sonst unbemerkt | Vorschlag: Review-Intervall je Inhalt festlegen (z. B. quartalsweise für Regulatorik) |

## 3. Redaktion und Governance

| # | Frage | Warum wichtig | Vorschlag / Stand |
|---|---|---|---|
| R1 | Fachreview: konkrete Personen | DoD verlangt Fachreview | **Vorläufig 2026-07-15:** Rollen definiert (Editorial / Insurance SME / Legal-Regulatory / Privacy-Security Reviewer, siehe `security-and-privacy-rules.md` §5.3); Personen noch zu benennen |
| R2 | Regulatorik-Review: konkrete Person (intern/extern, Jurist/in) | Pflicht für alle `REVIEW ERFORDERLICH: Regulatorik`-Inhalte | **Vorläufig 2026-07-15:** Rolle „Legal/Regulatory Reviewer“ definiert; ohne menschliche Freigabe keine Veröffentlichung kritischer Inhalte; Person noch zu benennen |
| R3 | Kennzeichnung KI-gestützt erstellter Inhalte gegenüber Lernenden? | Transparenz; ggf. regulatorische Anforderungen an KI-Transparenz | offen — REVIEW ERFORDERLICH: Regulatorik |
| R4 | Versionierung und Änderungshistorie von Inhalten für Lernende sichtbar? | Vertrauen, Nachvollziehbarkeit von Rechtsstand-Änderungen | offen |

## 4. Technik und Architektur

| # | Frage | Warum wichtig | Vorschlag / Stand |
|---|---|---|---|
| T1 | Technologie-Stack: Grundsatz-Architektur in ADR-0001 vorgeschlagen (Git-basiert, Variante A) — Bestätigung ausstehend; konkretes Framework/Hosting folgt als ADR-0002 | Grundsatzentscheidung | ADR-0001 zur Bestätigung — ENTSCHEIDUNG AUFTRAGGEBER |
| T2 | Content-Modell: Grundsatz (Markdown/MDX + schemavalidierte Strukturdaten) in ADR-0001 vorgeschlagen; Detail-Schemata folgen als ADR-0003 | Kern der Trennung Inhalt/Präsentation/Logik | Grundsatz in ADR-0001; Details offen |
| T3 | Detail-Abbildung der interaktiven Formate (Quiz, Simulationen, Ampel, Prompt-Bausatz) in Schemata | Bestimmt Autorenaufwand | offen — ADR-0003; deklarativ gemäß ADR-0001 |
| T4 | Accounts und Lernstandsspeicherung: mit Login, anonym, oder beides? | Datenschutzaufwand vs. Lernerlebnis | offen; datensparsamste tragfähige Variante bevorzugen |
| T5 | Hosting-Standort und Dienstleisterwahl (EU/DACH, AV-Verträge)? | Datenschutz, Drittlandtransfer | offen — REVIEW ERFORDERLICH: Regulatorik |
| T6 | Analytics/Reichweitenmessung: ob und womit? | Datenschutz, Consent-Management | offen; datensparsame Lösung bevorzugen |
| T7 | Suche über Inhalte: Eigenlösung oder Dienst? | Textplattform lebt von guter Suche | offen — Phase 2 |

## 5. Recht und Datenschutz

| # | Frage | Warum wichtig | Vorschlag / Stand |
|---|---|---|---|
| L1 | Impressums- und Datenschutzverantwortung (Herausgeber-Rechtsträger)? | Pflichtangaben der Plattform | offen — **Vorläufig 2026-07-15:** blockiert Produktivstart, nicht die Entwicklung; bis dahin klar gekennzeichnete Platzhalter (`security-and-privacy-rules.md` §5.2) |
| L2 | Speicher- und Löschfristen für Nutzer- und Lernstandsdaten? | Löschkonzept vor Implementierung nötig | **Vorläufig 2026-07-15:** Eckwerte festgelegt (Logs ≤ 14 Tage, Backups ≤ 30 Tage, Inaktivitätsprüfung 24 Monate; `security-and-privacy-rules.md` §5.1) — juristisch zu prüfen vor Produktivstart; Zertifikatsdaten nach Kontolöschung bleibt reviewpflichtig (DF1) |
| L3 | Nutzung von KI-APIs im Plattformbetrieb (nicht nur als Lerngegenstand): zulässig, welche Anbieter, welche Daten? | AV-Verträge, Drittlandtransfer, Kosten | offen — REVIEW ERFORDERLICH: Regulatorik |
| L4 | Haftungsausschluss / „keine Rechtsberatung“-Hinweis: Formulierung und Platzierung? | Absicherung bei regulatorischen Inhalten | offen; juristisch prüfen lassen |

## 6. Annahmen (zu validieren)

- `ANNAHME` A1: Lernende bevorzugen „Sie“-Anrede (siehe D1).
- `ANNAHME` A2: 10–20 Minuten pro Einheit passen zum Arbeitsalltag (siehe D2).
- `ANNAHME` A3: Rollenbasierte Lernpfade sind der richtige Hauptzuschnitt
  (statt Themenpfade wie „Prompting“, „Regulatorik“).
- `ANNAHME` A4: Deutsch als einzige Inhaltssprache reicht für den Start.
- `ANNAHME` A5: Die 10 definierten Rollen decken die Zielgruppe ausreichend
  ab; Nischenrollen (z. B. Aktuariat, Rückversicherung als eigene Rolle)
  können später ergänzt werden.
- `ANNAHME` A6: Ein textbasiertes, videofreies Angebot wird von der
  Zielgruppe als Vorteil (Tempo, Durchsuchbarkeit) wahrgenommen — durch
  Pilotfeedback prüfen.

## 7. Entschieden

| Datum | Entscheidung | Begründung / Referenz |
|---|---|---|
| 2026-07-14 | Plattform ist vollständig videofrei. | Produktvorgabe des Herausgebers; siehe `CLAUDE.md`, `docs/project-vision.md` |
| 2026-07-14 | Inhalts- und Dokumentationssprache Deutsch; Code und Commits Englisch. | Zielgruppe DACH; Entwickler-Konventionen; siehe `CLAUDE.md` |
| 2026-07-14 | Nur synthetische Übungsdaten, verbindliche Sicherheitsregeln. | Vorgabe des Herausgebers; siehe `docs/security-and-privacy-rules.md` |
| 2026-07-14 | Konzeption vor Implementierung: keine App, keine Kurse in Phase 0. | Vorgabe des Herausgebers; siehe `docs/project-vision.md` |
| 2026-07-14 | Geschäftsmodell: Freemium-Abo. | Entscheidung des Auftraggebers (P1); Details in `docs/product-requirements.md` |
| 2026-07-14 | Pilotkurs: rollenunabhängiger Grundkurs „KI-Führerschein für den Versicherungsalltag“ (7 Module). | Entscheidung des Auftraggebers (P2); Kursstruktur in `docs/product-requirements.md` |
| 2026-07-14 | Keine IDD-Weiterbildungszeit-Anrechnung angestrebt. | Entscheidung des Auftraggebers (P3); vereinfacht Prüfungs- und Nachweislogik |
| 2026-07-14 | Freemium-Grenze: Assessment + Modul 1 frei; Rest Premium (E1). | Bestätigung des Auftraggebers; `docs/product-requirements.md` Abschnitt 6 |
| 2026-07-14 | MVP ohne integrierte Bezahlstrecke: Premium per manueller Freischaltung; Preis/Anbieter später (E2/E2a). | Bestätigung des Auftraggebers; entkoppelt Marktstart von Zahlungsintegration |
| 2026-07-14 | Prompt-Werkstatt im MVP ohne Live-LLM-Anbindung, regelbasiertes Feedback (E4). | Bestätigung des Auftraggebers; L3 bleibt für Ausbaustufe offen |
| 2026-07-14 | Redaktions-Workflow Git-basiert, keine eigene Redaktions-UI im MVP (E5). | Bestätigung des Auftraggebers; prägt Architekturentscheidung (ADR-0001) |
| 2026-07-15 | **ADR-0001 bestätigt (Accepted):** Variante A — Git-basierte Inhalte, schlanke Anwendungsschicht, PostgreSQL mit Minimal-Nutzerdatenmodell. | Entscheidung des Auftraggebers; `docs/adr/0001-platform-architecture.md` |
| 2026-07-15 | Bestehensgrenze Abschlussprüfung: 80 % (E6). | Vorläufige Produktentscheidung des Auftraggebers |
| 2026-07-15 | Zertifikats-Verifikationslink: ja (E7). | Vorläufige Produktentscheidung des Auftraggebers |
| 2026-07-15 | Rollenfilter: einfacher Mehrfachfilter im MVP (E9). | Vorläufige Produktentscheidung des Auftraggebers |
| 2026-07-15 | Vorläufige Subdomain: `akademie.versicherungstech-magazin.de` (T8). | Vorläufige Produktentscheidung des Auftraggebers |
| 2026-07-15 | Keine nicht notwendige personenbezogene Drittanbieteranalyse im MVP (M-E3). | Vorläufige Produktentscheidung des Auftraggebers |
| 2026-07-15 | „War das hilfreich?“-Feedback: ja, datensparsam (M-E2). | Vorläufige Produktentscheidung des Auftraggebers |
| 2026-07-15 | Premium-Zugang über Berechtigungs-Flag; Mehrsprachigkeit technisch vorbereiten; MVP-Sprache Deutsch. | Vorläufige Produktentscheidungen des Auftraggebers; verankert in ADR-0001 |
| 2026-07-15 | Content-Schemata erst mit ADR-0003 finalisieren; Suchtechnik erst nach den Schemata entscheiden (ADR-0004). | Reihenfolge-Vorgabe des Auftraggebers |
| 2026-07-15 | Vorläufiges Löschkonzept, Platzhalter-Regel für Rechtstexte, vorläufige Review-Rollen. | Vorgaben des Auftraggebers; `security-and-privacy-rules.md` §5.1–5.3 — juristisch zu prüfen vor Produktivstart |
| 2026-07-15 | **ADR-0002 bestätigt (Accepted):** Astro + Svelte-Islands + Node-Adapter; Scalingo als Zielarchitektur (technisch akzeptiert, Anbieter rechtlich **nicht** freigegeben); H1–H7 als verpflichtende Produktivstart-Gates; Fallback-Reihenfolge Scalingo → Scaleway → Hetzner VM; nur stabile Framework-Versionen (Lockfile); keine automatische Produktion. | Entscheidung des Auftraggebers; `docs/adr/0002-framework-hosting.md` |
| 2026-07-15 | Zweitsicherung: Hetzner Object Storage als bevorzugter Kandidat — geplante, nicht aktivierte Produktionsanforderung. | Entscheidung des Auftraggebers; Aktivierungsbedingungen in ADR-0002 |
| 2026-07-15 | E-Mail: Scaleway TEM bleibt Kandidat; Auswahl zurückgestellt bis Prüfung (H7); keine Integration, kein Vertrag. | Entscheidung des Auftraggebers |
