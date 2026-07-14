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
| P6 | Freemium-Grenze: Welche Inhalte/Funktionen sind kostenlos, welche Premium? | Bestimmt Paywall-Logik, Conversion-Strategie und Content-Zuschnitt | Vorschlag in `docs/product-requirements.md` (Modul 1 + Assessment frei) — ENTSCHEIDUNG AUFTRAGGEBER |
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
| R1 | Wer übernimmt das Fachreview je Rolle (Namen/Verantwortliche)? | DoD verlangt Fachreview; ohne Personen kein Prozess | offen |
| R2 | Wer übernimmt das Regulatorik-Review (intern/extern, Jurist/in)? | Pflicht für alle `REVIEW ERFORDERLICH: Regulatorik`-Inhalte | offen |
| R3 | Kennzeichnung KI-gestützt erstellter Inhalte gegenüber Lernenden? | Transparenz; ggf. regulatorische Anforderungen an KI-Transparenz | offen — REVIEW ERFORDERLICH: Regulatorik |
| R4 | Versionierung und Änderungshistorie von Inhalten für Lernende sichtbar? | Vertrauen, Nachvollziehbarkeit von Rechtsstand-Änderungen | offen |

## 4. Technik und Architektur

| # | Frage | Warum wichtig | Vorschlag / Stand |
|---|---|---|---|
| T1 | Technologie-Stack (Framework, Hosting, ggf. statisch vs. dynamisch)? | Grundsatzentscheidung; als ADR zu dokumentieren | offen — Entscheidung in Phase 2 |
| T2 | Content-Modell: Markdown + strukturierte Metadaten, Headless CMS, oder eigenes Format? | Kern der Trennung Inhalt/Präsentation/Logik | offen — ADR nötig; Anforderungen: versionierbar, reviewfähig, interaktionsfähig |
| T3 | Wie werden interaktive Formate (Quiz, verzweigte Simulationen, Entscheidungsbäume) im Content-Modell abgebildet? | Bestimmt Autorenaufwand und Toolauswahl | offen; deklaratives Format (z. B. strukturierte Daten statt Code) anstreben |
| T4 | Accounts und Lernstandsspeicherung: mit Login, anonym, oder beides? | Datenschutzaufwand vs. Lernerlebnis | offen; datensparsamste tragfähige Variante bevorzugen |
| T5 | Hosting-Standort und Dienstleisterwahl (EU/DACH, AV-Verträge)? | Datenschutz, Drittlandtransfer | offen — REVIEW ERFORDERLICH: Regulatorik |
| T6 | Analytics/Reichweitenmessung: ob und womit? | Datenschutz, Consent-Management | offen; datensparsame Lösung bevorzugen |
| T7 | Suche über Inhalte: Eigenlösung oder Dienst? | Textplattform lebt von guter Suche | offen — Phase 2 |

## 5. Recht und Datenschutz

| # | Frage | Warum wichtig | Vorschlag / Stand |
|---|---|---|---|
| L1 | Impressums- und Datenschutzverantwortung (Herausgeber-Rechtsträger)? | Pflichtangaben der Plattform | offen |
| L2 | Speicher- und Löschfristen für Nutzer- und Lernstandsdaten? | Löschkonzept vor Implementierung nötig | offen — vor Phase 2 klären |
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
