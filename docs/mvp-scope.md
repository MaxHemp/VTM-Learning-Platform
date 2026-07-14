# MVP-Abgrenzung — VersicherungsTech KI-Akademie

**Status:** Entwurf zur Freigabe durch den Auftraggeber
**Stand:** 2026-07-14
**Grundlagen:** `docs/product-requirements.md`

Punkte mit Entscheidungsbedarf: **`ENTSCHEIDUNG AUFTRAGGEBER`** (E-Nummern
aus dem PRD, Abschnitt 13).

---

## 1. In Scope (MVP)

### Inhalte
- **Ein vollständiger Kurs:** „KI-Führerschein für den Versicherungsalltag“,
  7 Module, je 3–5 Einheiten à 10–20 Minuten, vollständig durch den
  Review-Workflow gelaufen (inkl. Regulatorik-Review für Modul 5 und
  Zertifikatstext).
- Prompt-Vorlagen-Bibliothek und Checklisten als Bestandteil der Module,
  einzeln auffindbar über die Suche.
- Rollen-Tagging aller Inhalte (Taxonomie der 10 Rollen).

### Funktionen (Lernende)
- Öffentliche Landingpage inkl. Rechtspflichtseiten
- Kurskatalog mit Kursdetailseite, Rollen- und Niveau-Filter (einfach — E9)
- Registrierung, Login, Passwort-Reset, Profil, Kontolöschung
- Freemium-Logik: freie vs. Premium-Inhalte (Grenze gemäß E1)
- Premium-Freischaltung (Bezahlstrecke oder manuell — E2/E2a)
- Einstufungsassessment (wiederholbar, optional)
- Persönlicher Lernpfad mit „Weiterlernen“-Einstieg
- Textbasierte Lektionen mit allen Inhaltselementen aus FR-5.2
- Quizze (4 Fragetypen, erklärendes Feedback, Modul-Checks)
- Verzweigte Fallsimulationen (2–4 Entscheidungsebenen)
- Datenampel-Übungen
- Prompt-Werkstatt (regelbasiert, ohne Live-LLM — E4)
- Lernfortschritt (Status, Prozent, geräteübergreifend)
- Abschlussprüfung mit Fragenpool und Prüfungssimulation
- Badges je Modul + PDF-Kurszertifikat (P7), einfache
  Zertifikatsverifikation (E7)
- Quellen-, Versions- und Rechtsstand-Anzeige an jedem Inhalt
- Volltextsuche mit Free/Premium-Kennzeichnung
- Mobile Darstellung und Barrierefreiheit (WCAG 2.1 AA-Orientierung)
  für alle genannten Funktionen

### Funktionen (intern)
- Redaktioneller Review-Workflow mit erzwungenem Regulatorik-Gate
  (Umsetzung voraussichtlich Git-basiert — E5)
- Automatisierte Content-Prüfungen im Build (Pflichtfelder, Marker-Logik,
  Blockade bei `QUELLE ZU VERIFIZIEREN`, kein Video-Inhaltstyp)
- Versionierung aller Inhalte
- Basis-Administration: Nutzer- und Premium-Verwaltung

## 2. Out of Scope (MVP) — bewusst nicht enthalten

| Ausschluss | Begründung |
|---|---|
| Weitere Kurse und rollenspezifische Vollpfade | Pilotfokus; Architektur ist darauf vorbereitet |
| Live-LLM-Anbindung in Übungen | Datenschutz-/Kostenfragen offen (L3, E4) |
| B2B-/Team-Funktionen (Mandanten, Team-Dashboards, Sammellizenzen) | Eigenes Datenschutzthema (NFR-D4); erst nach Freemium-Validierung |
| Community-Funktionen (Kommentare, Foren, Lerngruppen) | Moderationsaufwand; kein MVP-Kernnutzen |
| Eigene Redaktions-UI (CMS-Oberfläche) | Git-Workflow genügt für ein kleines Redaktionsteam (E5) |
| Native Apps (iOS/Android) | Responsive Web deckt mobile Nutzung ab |
| Offline-Nutzung | Ausbaustufe; Textformat macht es später gut machbar |
| Mehrsprachigkeit (EN, FR, IT) | Annahme A4: Deutsch reicht für den Start |
| IDD-Weiterbildungszeit-Anrechnung | Entschieden: entfällt (P3) |
| Gamification über Badges hinaus (Punkte, Ranglisten, Streaks) | Ranglisten kollidieren mit angstfreiem Lernen (US-10.2); ggf. später datensparsam |
| „Was ist neu“-Änderungsanzeige für Lernende | Interne Versionierung genügt im MVP (FR-13.4) |
| Personalisierte E-Mail-Lernerinnerungen | Double-Opt-in-Marketing-Thema; Ausbaustufe |
| Zahlungsanbieter-Integration, falls E2a = manuelle Freischaltung | Entkopplung des Marktstarts von der Bezahlstrecke |

## 3. Reduktionspfad bei Zeit-/Budgetdruck

Wenn der MVP-Umfang reduziert werden muss, wird in dieser Reihenfolge
gekürzt (nicht bei den Sicherheitsregeln — die sind unverhandelbar):

1. Zertifikatsverifikation per Link (E7) → Zertifikat ohne Verifikation
2. Badges je Modul → nur Kurszertifikat
3. Suchfilter (Rolle/Typ) → nur Volltextsuche
4. Rollenspezifische Beispiel-Varianten in Lektionen (FR-4.3) → einheitliche
   Beispiele
5. Zuordnungs-Fragetyp (Matching) im Quiz → drei Fragetypen
6. Einstufungsassessment → Selbstwahl des Einstiegs (Einsteiger/erfahren)

**Nicht kürzbar:** Datenampel, Fallsimulationen, Abschlussfall,
Quellen-/Versionsanzeige, Review-Workflow, Barrierefreiheit, mobile
Nutzung — sie tragen das Produktversprechen.

## 4. Voraussetzungen vor Implementierungsstart (Blocker)

| # | Voraussetzung | Referenz |
|---|---|---|
| V1 | Entscheidungen E1–E9 des Auftraggebers (mind. E1, E2a, E4, E5) | PRD Abschnitt 13 |
| V2 | Rechtsträger, Impressum, Datenschutzerklärung, ggf. AGB (juristisch) | L1, L4, E3 |
| V3 | Hosting-/Dienstleisterentscheidung inkl. AV-Verträge (EU-Präferenz) | T5 |
| V4 | Löschkonzept und Speicherfristen für Nutzerdaten | L2 |
| V5 | Fach- und Regulatorik-Reviewer benannt | R1/R2, E8 |
| V6 | Technologie-Stack und Content-Modell als ADRs | T1, T2, T3 |

## 5. Ausbaustufen nach dem MVP

### Ausbaustufe 1 — Vertiefen und Konvertieren
- Bezahlstrecke vollständig integriert (falls MVP mit manueller
  Freischaltung startete)
- Zweiter Kurs: erster rollenbezogener Vertiefungspfad
  (Rollenwahl datengetrieben: meistgewählte Rolle + Assessment-Daten;
  Vorschlag zur Prüfung: Schadenmanagement oder Kundenservice —
  ENTSCHEIDUNG AUFTRAGGEBER, wenn Daten vorliegen)
- Volle Facetten-Filter (Rolle × Niveau × Format) in Katalog und Suche
- „Was ist neu“-Anzeige bei aktualisierten Inhalten (Rechtsstand-Änderungen)
- E-Mail-Lernerinnerungen (Double-Opt-in)

### Ausbaustufe 2 — Interaktion und Werkzeuge
- Live-LLM-Anbindung der Prompt-Werkstatt (nach Klärung L3: Anbieter,
  AV-Vertrag, Kosten; nur mit synthetischen Übungsdaten)
- Weitere Übungstypen: interaktive Dokumentenübungen mit Annotation durch
  Lernende, längere verzweigte Simulationen, schriftliche Rollenspiele mit
  mehr Dialogtiefe
- Glossar als eigenständiger, verlinkter Nachschlagebereich
- Offline-Lesemodus

### Ausbaustufe 3 — Organisationen (B2B)
- Team-/Unternehmenslizenzen mit Mandantenfähigkeit
- Aggregierte, anonymisierte Team-Statistiken (streng datensparsam;
  kein Einzelpersonen-Tracking — Grundsatz aus NFR-D4 bleibt) —
  REVIEW ERFORDERLICH: Regulatorik
- Kuratierte Lernpläne durch Unternehmen
- SSO für Unternehmenskunden

### Ausbaustufe 4 — Skalierung des Curriculums
- Rollenpfade für alle 10 Rollen (3 Niveaus gemäß
  `docs/didactic-principles.md`)
- Rollenübergreifende Basismodule als wiederverwendbare Bausteine
- Regelmäßige Regulatorik-Updates als eigenes Inhaltsformat
  („Rechtsstand-Briefings“)
- Redaktions-UI, falls das Redaktionsteam wächst

## 6. Explizite Nicht-Ziele (dauerhaft, aus der Projektvision)

- Keine Videoformate — in keiner Ausbaustufe.
- Keine Rechtsberatung.
- Kein Verkauf oder Bewerbung einzelner KI-Tools.
- Keine Darstellung von KI als alleinige Entscheidungsinstanz.
- Keine Leistungsüberwachung von Lernenden durch Dritte.
