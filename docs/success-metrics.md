# Messgrößen — MVP der VersicherungsTech KI-Akademie

**Status:** Entwurf zur Freigabe durch den Auftraggeber
**Stand:** 2026-07-14
**Grundlagen:** `docs/product-requirements.md`, `docs/project-vision.md`

## 1. Grundsätze der Messung

- **Datensparsamkeit vor Messtiefe:** Gemessen wird nur, was eine konkrete
  Produktentscheidung informiert. Kein Tracking ohne Rechtsgrundlage
  (NFR-D3); Analytics-Lösung ist offen (T6) — die Messgrößen hier sind so
  gewählt, dass sie überwiegend aus eigenen Bestandsdaten (Accounts,
  Fortschritt, Abos) ableitbar sind.
- **Kein Personen-Ranking:** Alle Auswertungen aggregiert; niemals
  Leistungsvergleich einzelner Lernender (Grundsatz aus NFR-D4/US-10.2).
- **Zielwerte sind Hypothesen:** Die Zahlen unten sind Startwerte zur
  Kalibrierung, keine Zusagen. Nach 3 Monaten Review und Anpassung.
  **ENTSCHEIDUNG AUFTRAGGEBER:** Zielwerte bestätigen oder anpassen (M-E1).

## 2. Nordstern-Metrik

**Anzahl Lernender, die die Abschlussprüfung bestehen**
(„ausgestellte KI-Führerscheine“ pro Monat).

Begründung: Diese eine Zahl setzt voraus, dass Akquise, Aktivierung,
Conversion, Inhaltsqualität und Prüfungsdidaktik gemeinsam funktionieren —
sie ist gegen Einzeloptimierung (z. B. reine Registrierungszahlen) robust
und entspricht dem Produktversprechen.

## 3. Messgrößen je Trichterstufe

### 3.1 Akquise (Landingpage, Katalog)

| Metrik | Definition | Startziel (Hypothese) |
|---|---|---|
| Besucher → Registrierung | Anteil der Landingpage-Besucher, die ein Konto anlegen | ≥ 3 % |
| Katalog → Kursstart (Gast → Modul-1-Vorschau/Registrierung) | Anteil der Kursdetail-Besucher, die den Einstieg beginnen | ≥ 15 % |

Hinweis: Besucherzahlen setzen eine datenschutzkonforme Reichweitenmessung
voraus (T6) — bis dahin nur registrierungsbasierte Messung.

### 3.2 Aktivierung (Assessment, Lernstart)

| Metrik | Definition | Startziel |
|---|---|---|
| Aktivierungsquote | Anteil Registrierter, die innerhalb von 7 Tagen mindestens eine Lerneinheit abschließen | ≥ 50 % |
| Assessment-Nutzung | Anteil Registrierter, die das Einstufungsassessment abschließen | ≥ 60 % |
| Modul-1-Abschluss | Anteil Registrierter, die Modul 1 vollständig abschließen | ≥ 35 % |

### 3.3 Engagement und Lernerfolg

| Metrik | Definition | Startziel |
|---|---|---|
| Fortsetzungsquote | Anteil der Lernenden, die nach einer abgeschlossenen Einheit innerhalb von 14 Tagen die nächste beginnen | ≥ 60 % |
| Kursabschlussquote (Premium) | Anteil Premium-Lernender, die alle 7 Module abschließen | ≥ 40 % |
| Bestehensquote Abschlussprüfung | Anteil der Prüfungsteilnahmen, die bestehen (Erst- und Wiederholungsversuche getrennt ausweisen) | 60–85 % Korridor* |
| Einheitendauer | Median der Bearbeitungszeit je Einheit (nur aggregiert) | 10–20 Min. (validiert Annahme A2/D2) |
| Suche-Nutzung | Anteil aktiver Lernender, die die Suche mindestens einmal pro Monat nutzen | ≥ 25 % (validiert Nachschlagewerk-These J10) |

*Deutlich über 85 % → Prüfung zu leicht; deutlich unter 60 % → Inhalte oder
Prüfung überarbeiten. Der Korridor misst die Prüfungskalibrierung, nicht die
Lernenden.

### 3.4 Monetarisierung (Freemium)

| Metrik | Definition | Startziel |
|---|---|---|
| Free→Premium-Conversion | Anteil der Free-Konten, die innerhalb von 30 Tagen Premium abschließen | ≥ 5 % |
| Conversion nach Modul-1-Abschluss | Anteil der Modul-1-Absolventen, die Premium abschließen | ≥ 15 % (misst die Freemium-Grenze E1) |
| Kündigungsquote (Churn) | Anteil der Premium-Abos, die im Monat gekündigt werden | Beobachten; Zielwert nach 3 Monaten (M-E1) |

### 3.5 Qualität und Vertrauen

| Metrik | Definition | Startziel |
|---|---|---|
| Einheiten-Feedback | Einfache Rückmeldung je Einheit („War das hilfreich?“ + optionales Freitextfeld) | ≥ 80 % positiv |
| Inhaltsfehler-Meldungen | Anzahl gemeldeter fachlicher/regulatorischer Fehler in veröffentlichten Inhalten | 0 kritische; jede Meldung < 14 Tage bearbeitet |
| Review-Durchlaufzeit | Zeit von „Fachreview angefragt“ bis Freigabe/Rückweisung | Median ≤ 10 Werktage (misst Review-Engpass R4) |
| Rechtsstand-Aktualität | Anteil veröffentlichter Regulatorik-Inhalte, deren letztes Review nicht älter ist als das definierte Intervall (D6) | 100 % |

### 3.6 Technische Qualität

| Metrik | Definition | Startziel |
|---|---|---|
| Mobile Nutzbarkeit | Anteil der Lerneinheiten-Abschlüsse auf mobilen Viewports | Beobachten (validiert NFR-B; erwartbar ≥ 25 %) |
| Ladezeit | Inhaltsseiten interaktiv auf 4G/Mittelklasse-Gerät | ≤ ~3 s (NFR-C1) |
| Barrierefreiheits-Befunde | Offene Befunde aus a11y-Prüfung (automatisiert + manuelle Stichprobe) | 0 Blocker vor Launch |
| Verfügbarkeit | Erreichbarkeit werktags 6–22 Uhr | Beobachten; SLO in Phase 2 |

## 4. Validierung der Kernannahmen

| Annahme | Messgröße | Entscheidung bei Nichtbestätigung |
|---|---|---|
| A2: 10–20-Min.-Einheiten passen | Einheitendauer, Abbruchpunkte innerhalb von Einheiten | Einheiten kürzen/teilen |
| A6: Videofreies Format wird als Vorteil wahrgenommen | Einheiten-Feedback, Kursabschlussquote, qualitative Pilotinterviews | Textformate stärken (mehr Interaktion), nicht Video einführen — Nicht-Ziel bleibt |
| E1: Freemium-Grenze richtig | Conversion nach Modul-1-Abschluss vs. Aktivierungsquote | Grenze verschieben (mehr/weniger frei) |
| A3: Rollenunabhängiger Einstieg trägt | Rollenverteilung der Registrierungen, Feedback der Spezialisten-Personas (R7) | Rollenvarianten in Lektionen ausbauen; Rollenpfad vorziehen |

## 5. Berichtsrhythmus

- **Wöchentlich (intern, automatisierbar):** Registrierungen, Aktivierung,
  Conversion, Prüfungen, kritische Fehler-Meldungen.
- **Monatlich (Auftraggeber):** Nordstern, Trichter-Übersicht,
  Qualitätsmetriken, Annahmen-Status, Empfehlungen.
- **Nach 3 Monaten:** Review aller Zielwerte (M-E1), Entscheidung über
  Ausbaustufe 1.

## 6. Entscheidungsbedarf des Auftraggebers

| # | Entscheidung |
|---|---|
| M-E1 | Zielwerte in Abschnitt 3 bestätigen oder anpassen; Churn-Zielwert nach 3 Monaten festlegen |
| M-E2 | Freigabe der „War das hilfreich?“-Rückmeldung je Einheit (einzige zusätzliche Datenerhebung über Bestandsdaten hinaus; anonym auswertbar) |
| M-E3 | Auswahl der datenschutzkonformen Reichweitenmessung (T6) oder bewusster Verzicht im MVP |
