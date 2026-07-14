# Definition of Done — VersicherungsTech KI-Akademie

**Status:** Entwurf · Konzeptionsphase
**Stand:** 2026-07-14

Diese Definition of Done (DoD) gilt für drei Arbeitstypen: **Lerninhalte**,
**Code** und **Dokumentation/ADRs**. Ein Arbeitsergebnis ist erst „done“,
wenn alle zutreffenden Punkte erfüllt sind.

## 1. DoD für Lerninhalte

### Fachlich und didaktisch

- [ ] Zielrolle(n) und Niveau (Grundlagen/Anwendung/Vertiefung) sind benannt.
- [ ] Nutzenversprechen ist konkret und rollenbezogen formuliert.
- [ ] Struktur folgt dem Redaktionsleitfaden (Nutzenversprechen → Kerninhalt
      → Praxisteil → Grenzen & Kontrolle → Zusammenfassung → Transferaufgabe).
- [ ] Mindestens ein anwendbares Praxiselement ist enthalten (Vorlage,
      Checkliste, Übung, Simulation o. ä.).
- [ ] Eine Transferaufgabe für den eigenen Arbeitskontext ist enthalten.
- [ ] Alle Interaktionen (Quiz, Simulation) geben erklärendes Feedback.
- [ ] Die Einheit ist im Zielzeitrahmen (ca. 10–20 Min.) absolvierbar.

### Format und Tonalität

- [ ] Format ist zulässig: **kein Video, kein Video-Platzhalter, keine
      Video-Abhängigkeit**.
- [ ] Tonalität eingehalten: kompakt, verständlich, praxisnah, fachlich,
      umsetzungsorientiert; keine Marketingfloskeln, kein unnötiger Jargon.
- [ ] Fachbegriffe sind bei Erstverwendung erklärt, Abkürzungen ausgeschrieben.

### Sicherheit und Regulatorik

- [ ] Nur synthetische Übungsdaten; Kennzeichnung `SYNTHETISCHE DATEN`
      vorhanden.
- [ ] Keine realistisch wirkenden vollständigen Identitäten.
- [ ] Rechtliche/regulatorische Aussagen haben Quelle + Fundstelle +
      `RECHTSSTAND: JJJJ-MM-TT`.
- [ ] Marker `REVIEW ERFORDERLICH: Regulatorik` gesetzt, wo zutreffend —
      und das Review ist **erfolgt**, bevor der Inhalt als veröffentlichbar
      gilt.
- [ ] Keine unverifizierten Quellen ohne Marker `QUELLE ZU VERIFIZIEREN`;
      vor Veröffentlichung sind alle solchen Marker aufgelöst.
- [ ] Keine „automatisch AI-Act-/DSGVO-konform“-Behauptungen.
- [ ] Bei entscheidungsnahen oder kundenrelevanten KI-Beispielen:
      menschlicher Kontrollpunkt mit Wer/Was/Wann/Wie definiert.
- [ ] KI ist nirgends alleinige Instanz für Deckung, Leistung, Pricing,
      Underwriting, Betrugsverdacht oder Kundenberatung.

### Prozess

- [ ] Fachreview durch Person mit Rollenexpertise ist erfolgt.
- [ ] Redaktionsfreigabe ist erfolgt.

## 2. DoD für Code

### Qualität

- [ ] Code erfüllt die Aufgabe nachweislich (manuell verifiziert oder durch
      Tests belegt).
- [ ] Neue Logik ist durch automatisierte Tests abgedeckt; bestehende Tests
      laufen grün.
- [ ] Linter/Formatter des Projekts laufen ohne Fehler (sobald konfiguriert).
- [ ] Nicht offensichtliche Entscheidungen und öffentliche Schnittstellen
      sind dokumentiert.

### Architektur

- [ ] Trennung von Inhalt, Präsentation und Anwendungslogik ist eingehalten.
- [ ] Keine unbegründete Abweichung von bestehender Architektur; wesentliche
      Architekturentscheidungen sind als ADR unter `docs/adr/` dokumentiert.
- [ ] Änderung ist in kleine, nachvollziehbare Commits mit klaren Messages
      zerlegt.

### Sicherheit und Datenschutz

- [ ] Keine Secrets im Code, in Konfiguration oder Git-Historie; Geheimnisse
      über Umgebungsvariablen.
- [ ] Datensparsamkeit: keine Erhebung von Nutzerdaten ohne definierten Zweck.
- [ ] Keine realen personenbezogenen Daten in Fixtures, Tests oder Seeds —
      nur synthetische Daten.

### Barrierefreiheit und Nutzung

- [ ] UI-Änderungen sind per Tastatur bedienbar und screenreader-tauglich
      (semantisches HTML, Labels, Fokusreihenfolge).
- [ ] Kontraste und Textgrößen orientieren sich an WCAG 2.1 AA.
- [ ] Ansicht ist auf mobilen Bildschirmgrößen geprüft.

### Prozess

- [ ] Änderung wurde auf dem vorgesehenen Branch entwickelt und gepusht.
- [ ] Kein Deployment ohne ausdrückliche Freigabe.

## 3. DoD für Dokumentation und ADRs

- [ ] Dokument hat Status (Entwurf/verbindlich), Stand (Datum) und klaren
      Geltungsbereich.
- [ ] Annahmen sind als `ANNAHME` gekennzeichnet.
- [ ] Offene Punkte sind in `docs/open-questions.md` eingetragen statt
      stillschweigend offen zu bleiben.
- [ ] Querverweise auf verwandte Dokumente sind vorhanden und korrekt.
- [ ] ADRs enthalten: Kontext, Entscheidung, Alternativen, Konsequenzen.

## 4. Ausnahmen

Abweichungen von dieser DoD sind möglich, müssen aber im Commit, PR oder
Dokument ausdrücklich benannt und begründet werden. Nicht verhandelbar sind
die Sicherheitsregeln (Abschnitt „Sicherheit und Regulatorik“ bzw.
`docs/security-and-privacy-rules.md`).
