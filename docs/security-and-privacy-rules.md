# Sicherheits- und Datenschutzregeln — VersicherungsTech KI-Akademie

**Status:** Verbindlich (Arbeitsfassung) · Konzeptionsphase
**Stand:** 2026-07-14

Diese Regeln sind für alle Inhalte, Übungen, Werkzeuge und Code in diesem
Repository verbindlich. Bei Konflikten zwischen Geschwindigkeit und diesen
Regeln gewinnen die Regeln.

## 1. Übungs- und Beispieldaten

### 1.1 Nur synthetische Daten

- Alle Übungs- und Beispieldaten sind **synthetisch** (erfunden).
- Synthetische Datensätze werden gekennzeichnet mit:
  **`SYNTHETISCHE DATEN — Alle Personen, Firmen und Fälle sind frei
  erfunden.`**
- Reale Fälle dürfen auch in „anonymisierter“ Form **nicht** als Grundlage
  dienen — Anonymisierung realer Kundendaten ist fehleranfällig und wird
  hier nicht praktiziert.

### 1.2 Keine realistisch wirkenden vollständigen Identitäten

- Keine Kombinationen, die wie eine reale Person wirken (echt klingender
  Vollname + Adresse + Geburtsdatum + Vertrags-/Gesundheits-/Schadendaten).
- Beispielpersonen bleiben erkennbar generisch: reduzierte Attribute,
  fiktive Muster (z. B. „A. Muster, 43, angestellt, PLZ-Raum 5xxxx“),
  fiktive Firmennamen („Musterversicherung AG“).
- Keine realen Adressen, IBANs, Versicherungsschein- oder Schadennummern
  realer Gesellschaften; erkennbar fiktive Formate verwenden
  (z. B. `VSN-TEST-000123`).

### 1.3 Verbotene Datenkategorien

In Repository, Inhalten und Übungen sind ausgeschlossen:

- reale Kundendaten jeder Art
- reale Gesundheitsdaten
- reale Schadendaten
- reale Vertragsdaten
- reale personenbezogene Daten von Mitarbeitenden, Testpersonen oder
  Interviewpartnern (außer dokumentierte, freigegebene Namensnennungen,
  z. B. Autorenschaft)

## 2. Secrets und Zugangsdaten

- **Keine Secrets im Repository:** keine API-Keys, Passwörter, Tokens,
  Zertifikate, Verbindungsstrings — auch nicht in Beispielen, Tests,
  Kommentaren oder der Git-Historie.
- Geheimnisse werden über **Umgebungsvariablen** bereitgestellt.
- `.env`-Dateien stehen in `.gitignore`; als Vorlage dient `.env.example`
  mit Variablennamen ohne Werte.
- In Lerninhalten gezeigte Beispiel-Keys sind offensichtlich fiktiv
  (z. B. `sk-BEISPIEL-NICHT-ECHT`).
- Wird versehentlich ein Secret committet: sofort melden, Secret beim
  Anbieter widerrufen/rotieren; das bloße Entfernen aus dem aktuellen Stand
  genügt nicht (Git-Historie).

## 3. Regulatorische und rechtliche Aussagen

- Keine rechtlich verbindlichen Aussagen ohne **Quelle und Rechtsstand**
  (`RECHTSSTAND: JJJJ-MM-TT`).
- Inhalte mit regulatorischen Aussagen tragen den Marker
  **`REVIEW ERFORDERLICH: Regulatorik`** und gelten bis zur Freigabe durch
  eine fachlich zuständige Person als Entwurf.
- **Primärquellen bevorzugen:** EUR-Lex, nationale Gesetzestexte,
  BaFin/FMA/FINMA, EIOPA, EDSA/DSK.
- **Keine erfundenen Quellen**, Fundstellen, Gerichtsurteile oder
  Behördenaussagen. Nicht verifizierbare Quellen: **`QUELLE ZU VERIFIZIEREN`**.
- Niemals behaupten, ein Kurs, Prozess oder System sei automatisch
  „AI-Act-konform“ oder „DSGVO-konform“. Konformität ist eine
  einzelfallbezogene, fortlaufende organisatorische Aufgabe — Inhalte
  können dabei *unterstützen*, mehr nicht.
- Die Akademie leistet keine Rechtsberatung; ein entsprechender Hinweis
  gehört an regulatorische Inhalte.

## 4. Darstellung von KI in Inhalten und Beispielen

### 4.1 KI ist nie alleinige Instanz

KI wird niemals als alleinige Entscheidungsinstanz dargestellt für:

- Deckung
- Leistung
- Pricing
- Underwriting
- Betrugsverdacht
- Kundenberatung

### 4.2 Menschlicher Kontrollpunkt ist Pflicht

Jede kundenrelevante oder entscheidungsnahe KI-Anwendung in Lerninhalten
definiert einen menschlichen Kontroll- oder Freigabepunkt mit vier Angaben:

1. **Wer** prüft (Rolle)?
2. **Was** wird geprüft (Prüfgegenstand, Kriterien)?
3. **Wann** wird geprüft (vor welcher Wirkung nach außen)?
4. **Wie** kann eingegriffen werden (ändern, ablehnen, eskalieren)?

### 4.3 Ehrliche Fähigkeitsdarstellung

- Fehlermodi (Halluzination, veraltetes Wissen, Bias, fehlender Kontext)
  werden dort benannt, wo sie praktisch relevant sind.
- Keine Suggestion, KI-Ergebnisse seien ungeprüft verwendbar.

## 5. Datenschutz der Plattform (für spätere Implementierung)

Diese Anforderungen fließen in die technische Architektur ein:

- **Datensparsamkeit:** Es werden nur Daten erhoben, die für Lernbetrieb
  und gesetzliche Pflichten erforderlich sind.
- **Zweckbindung:** Lernstandsdaten dienen dem Lernen der Nutzerinnen und
  Nutzer; eine Nutzung für Leistungsbewertung durch Arbeitgeber ist nicht
  vorgesehen und wäre gesondert zu bewerten (`REVIEW ERFORDERLICH:
  Regulatorik`).
- **Transparenz:** Datenschutzerklärung mit Verarbeitungszwecken,
  Rechtsgrundlagen, Speicherdauern; verständlich formuliert.
- **Löschkonzept:** Speicher- und Löschfristen werden vor Implementierung
  definiert. Vorläufige Eckwerte siehe Abschnitt 5.1.
- **Auftragsverarbeitung:** Externe Dienste (Hosting, Analytics, KI-APIs)
  nur mit AV-Vertrag und Prüfung von Drittlandtransfers.
- **Tracking:** Kein Tracking ohne Rechtsgrundlage; Reichweitenmessung
  möglichst datensparsam.
- Offene Datenschutzentscheidungen: siehe `docs/open-questions.md`.

### 5.1 Vorläufiges Löschkonzept

**Status: VORLÄUFIG (Vorgabe des Auftraggebers, 2026-07-15) —
juristisch zu prüfen vor Produktivstart. REVIEW ERFORDERLICH: Regulatorik.**

- **Technische Sicherheitslogs:** maximal **14 Tage**, sofern kein
  dokumentierter Sicherheitsvorfall eine längere Aufbewahrung erfordert.
- **Anwendungslogs:** keine Lernprompts, keine Übungsfreitexte, keine
  Zugangsdaten, keine sensiblen Inhalte in Anwendungslogs.
- **Backups:** vorläufig maximal **30 Tage** Aufbewahrung.
- **Inaktive Nutzerkonten:** Löschprüfung nach **24 Monaten** Inaktivität.
- **Kontolöschung:** Nutzerinnen und Nutzer müssen eine Kontolöschung
  anfordern können (Selbstbedienung gemäß FR-16.5).
- **Zertifikatsdaten nach Kontolöschung:** Umgang bleibt reviewpflichtig
  (offene Frage DF1/L2); keine Vorwegnahme durch die Implementierung.
- **Technische Anforderung an das Datenmodell:** Löschung, Anonymisierung,
  Deaktivierung und **Widerruf eines Zertifikats** müssen technisch
  unterstützt werden.

### 5.2 Rechtstexte (vorläufige Regelung)

**Status: VORLÄUFIG (Vorgabe des Auftraggebers, 2026-07-15).**

- Impressum, Datenschutzerklärung und ggf. AGB **blockieren den
  Produktivstart**, aber nicht die lokale Entwicklung.
- Bis zur juristischen Freigabe werden ausschließlich **klar
  gekennzeichnete Platzhalter** verwendet (z. B.
  „PLATZHALTER — RECHTSTEXT NICHT FREIGEGEBEN“).
- KI-generierte Rechtstexte werden **niemals** als final oder rechtlich
  freigegeben dargestellt.

### 5.3 Review-Rollen (vorläufig, bis Personen benannt sind)

**Status: VORLÄUFIG (Vorgabe des Auftraggebers, 2026-07-15).**

| Rolle | Zuständigkeit |
|---|---|
| Editorial Reviewer | Redaktionsleitfaden, Tonalität, Didaktik-Struktur |
| Insurance Subject-Matter Reviewer | Fachliche Korrektheit (Versicherung) |
| Legal/Regulatory Reviewer | Alle Inhalte mit `REVIEW ERFORDERLICH: Regulatorik`, Rechtstexte, Zertifikatstext |
| Privacy/Security Reviewer | Datenschutz-/Sicherheitsrelevante Inhalte, Datenmodell-Änderungen, Threat-Model-Pflege |

Ohne die jeweilige **menschliche** Freigabe dürfen fachlich oder
regulatorisch kritische Inhalte nicht veröffentlicht werden. Die
Benennung konkreter Personen steht aus (offene Frage R1/R2).

## 6. Praktische Übungen mit KI-Tools

- Übungen nutzen nur **freigegebene KI-Tools** (Freigabeliste ist noch zu
  erstellen — siehe `docs/open-questions.md`).
- In Übungsanleitungen wird ausdrücklich darauf hingewiesen, **keine realen
  Kunden- oder Unternehmensdaten** in KI-Tools einzugeben; es werden
  bereitgestellte synthetische Übungsdaten verwendet.
- Übungen erklären, dass Eingaben in externe KI-Dienste die eigene
  Organisation verlassen können, und verweisen auf interne Richtlinien der
  Lernenden.

## 7. Sicherheit im Entwicklungsprozess

- Abhängigkeiten werden bewusst gewählt und aktuell gehalten.
- Keine destruktiven Befehle (Datenlöschung, Force-Push, Branch-Löschung)
  ohne ausdrückliche Bestätigung.
- Kein Deployment ohne ausdrückliche Freigabe.
- Sicherheitsrelevante Architekturentscheidungen werden als ADR unter
  `docs/adr/` dokumentiert.

## 8. Meldung von Verstößen

Wer einen Verstoß gegen diese Regeln bemerkt (z. B. reale Daten in einer
Übung, ein Secret im Repository, eine unbelegte Rechtsaussage), meldet ihn
umgehend an die Projektleitung und dokumentiert ihn in
`docs/open-questions.md` oder einem Issue. Betroffene Inhalte werden bis
zur Klärung nicht veröffentlicht.
