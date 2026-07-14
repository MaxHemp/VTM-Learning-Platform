# Redaktionsleitfaden — VersicherungsTech KI-Akademie

**Status:** Entwurf · Konzeptionsphase
**Stand:** 2026-07-14

Dieser Leitfaden gilt für alle Lerninhalte, Übungen, Vorlagen und
Plattformtexte. Er ergänzt die verbindlichen Regeln in `CLAUDE.md` und
`docs/security-and-privacy-rules.md`.

## 1. Tonalität

Alle Texte sind:

- **kompakt** — kein Satz ohne Funktion; Redundanz nur, wenn sie didaktisch
  gewollt ist (z. B. Zusammenfassungen).
- **verständlich** — kurze Sätze, aktive Formulierungen, ein Gedanke pro
  Absatz.
- **praxisnah** — jedes Konzept wird an einem Versicherungsbeispiel gezeigt.
- **fachlich** — korrekte Branchenterminologie; keine Vereinfachung, die
  fachlich falsch wird.
- **umsetzungsorientiert / Hands-on** — Leserinnen und Leser wissen nach
  jedem Abschnitt, was sie damit tun können.

**Nicht erlaubt:**

- Marketingfloskeln („revolutionär“, „Game-Changer“, „die Zukunft ist jetzt“)
- unnötiger Technikjargon; wo ein Fachbegriff nötig ist, wird er bei
  Erstverwendung in einem Satz erklärt
- Angstrhetorik („Wer KI nicht nutzt, verschwindet vom Markt“)
- pauschale Heilsversprechen („KI löst Ihr Schadenmanagement“)

## 2. Sprache und Stil

- **Sprache:** Deutsch. Etablierte englische Fachbegriffe (Prompt, Large
  Language Model, Underwriting) bleiben englisch; erfundene Anglizismen
  werden vermieden.
- **Anrede:** Lernende werden mit „Sie“ angesprochen (Annahme — zu
  bestätigen, siehe `docs/open-questions.md`).
- **Geschlechtergerechte Sprache:** neutrale Formulierungen bevorzugen
  („Mitarbeitende“, „Vermittlerinnen und Vermittler“); konsistent pro
  Dokument.
- **Zahlen und Daten:** Zahlen mit Quelle und Datum; keine ungefähren
  Behauptungen („die meisten Versicherer…“) ohne Beleg.
- **Abkürzungen:** bei Erstverwendung ausschreiben, danach abkürzen
  (z. B. „Datenschutz-Grundverordnung (DSGVO)“).
- **DACH-Differenzierung:** Aussagen, die nur für ein Land gelten, werden
  gekennzeichnet (z. B. „gilt in Deutschland; für Österreich/Schweiz siehe …“).

## 3. Struktur von Lerninhalten

Jede Lektion folgt einer wiedererkennbaren Grundstruktur:

1. **Nutzenversprechen (2–3 Sätze):** Was kann ich danach, warum ist das
   für meine Rolle relevant?
2. **Kerninhalt:** kompakt, mit Zwischenüberschriften, Beispielen und
   annotierten Auszügen.
3. **Praxisteil:** mindestens ein anwendbares Element (Prompt-Vorlage,
   Checkliste, Übung, Fallsimulation).
4. **Grenzen und Kontrolle:** Was kann die KI hier nicht? Wo prüft ein
   Mensch? (Pflichtabschnitt bei entscheidungsnahen Themen.)
5. **Zusammenfassung:** 3–5 Merksätze.
6. **Transferaufgabe:** konkreter Arbeitsauftrag für den eigenen Kontext.

## 4. Quellenarbeit

- **Primärquellen bevorzugen:** Gesetzestexte (EUR-Lex, Bundesgesetzblätter),
  Aufsichtsbehörden (BaFin, FMA, FINMA, EIOPA), Datenschutzgremien
  (EDSA, DSK), offizielle Dokumentationen von Herstellern.
- **Jede regulatorische oder rechtliche Aussage** trägt: Quelle, Fundstelle
  und **Rechtsstand (Datum)**.
- **Keine erfundenen Quellen.** Keine erfundenen Urteile, Aktenzeichen,
  Behördenaussagen oder Statistiken — im Zweifel weglassen.
- Nicht verifizierbare Quellen kennzeichnen: **`QUELLE ZU VERIFIZIEREN`**.
- Sekundärquellen (Studien, Fachartikel) sind zulässig für Einordnung und
  Marktbeobachtung, nicht als Beleg für Rechtsaussagen.

## 5. Kennzeichnungen (Pflicht-Marker)

| Marker | Bedeutung |
|---|---|
| `REVIEW ERFORDERLICH: Regulatorik` | Inhalt enthält regulatorische/rechtliche Aussagen und braucht fachliche Freigabe vor Veröffentlichung. |
| `QUELLE ZU VERIFIZIEREN` | Quelle konnte nicht verifiziert werden. |
| `SYNTHETISCHE DATEN` | Übungsdaten sind erfunden; jede Ähnlichkeit mit realen Personen oder Fällen ist zufällig. |
| `RECHTSSTAND: JJJJ-MM-TT` | Datum, auf das sich rechtliche Aussagen beziehen. |
| `ANNAHME` | Arbeitshypothese, noch nicht validiert. |

Marker stehen sichtbar am Inhalt (nicht nur in Metadaten), solange kein
technisches Kennzeichnungssystem existiert.

## 6. Umgang mit KI-Aussagen

- Fähigkeiten von KI-Werkzeugen werden **konkret und begrenzt** beschrieben
  („kann Entwürfe für Standardkorrespondenz erstellen“), nicht pauschal
  („versteht Ihre Kunden“).
- Fehlermodi gehören dazu: Halluzinationen, veraltetes Wissen, Verzerrungen
  (Bias), Datenschutzrisiken werden dort benannt, wo sie praktisch relevant
  sind.
- KI wird nie als alleinige Entscheidungsinstanz für Deckung, Leistung,
  Pricing, Underwriting, Betrugsverdacht oder Kundenberatung dargestellt.
  Jedes entscheidungsnahe Beispiel benennt den menschlichen Kontrollpunkt.
- Herstellerneutralität: Tools werden als Beispiele behandelt; Vor- und
  Nachteile werden benannt; keine Werbesprache.

## 7. Beispiele und Übungsdaten

- Ausschließlich **synthetische Daten** (Details:
  `docs/security-and-privacy-rules.md`).
- Beispielfirmen und -personen sind erkennbar fiktiv (z. B.
  „Musterversicherung AG“, „Vermittlerbüro Beispiel & Partner“).
- Keine realistisch wirkenden vollständigen Identitäten; keine realen
  Kunden-, Gesundheits-, Schaden- oder Vertragsdaten — auch nicht
  anonymisiert aus realen Fällen abgeleitet.

## 8. Review-Prozess (Arbeitsfassung)

1. **Autor/in bzw. KI-Entwurf** → Selbstprüfung gegen diesen Leitfaden.
2. **Fachreview** durch eine Person mit Branchenexpertise der Zielrolle.
3. **Regulatorik-Review** für alle Inhalte mit Marker
   `REVIEW ERFORDERLICH: Regulatorik`.
4. **Redaktionsfreigabe** durch die Redaktion des VersicherungsTech Magazins.

Rollen und Verantwortliche sind noch zu besetzen — siehe
`docs/open-questions.md`.
