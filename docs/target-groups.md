# Zielgruppen — VersicherungsTech KI-Akademie

**Status:** Entwurf · Konzeptionsphase
**Stand:** 2026-07-14

## 1. Überblick

Die KI-Akademie richtet sich an Menschen aus der **DACH-Versicherungsbranche**
(Deutschland, Österreich, Schweiz). Zielgruppe sind Fachkräfte, die KI in
ihrer täglichen Arbeit einsetzen wollen oder sollen — unabhängig von
technischer Vorbildung.

### Organisationstypen

- Versicherer (Erst- und Rückversicherer)
- Agenturen
- Makler
- Assekuradeure
- InsurTechs
- versicherungsnahe Dienstleister (z. B. Schadendienstleister,
  Softwareanbieter, Beratungen)

## 2. Rollenprofile

Für jede Rolle gilt: Die Profile beschreiben typische Aufgaben und
KI-Berührungspunkte. Sie sind Arbeitshypothesen und werden durch
Nutzerfeedback validiert (siehe `docs/open-questions.md`).

### 2.1 Vertrieb

- **Typische Aufgaben:** Kundenakquise, Angebotserstellung, Bedarfsanalyse,
  Terminvorbereitung, Bestandsausbau.
- **KI-Berührungspunkte:** Recherche- und Textassistenz, Gesprächs-
  vorbereitung, Angebotsentwürfe, Zusammenfassungen.
- **Besondere Anforderungen:** Beratungspflichten und Dokumentation (u. a.
  IDD-Kontext) — KI unterstützt die Vorbereitung, ersetzt keine Beratung.

### 2.2 Kundenservice

- **Typische Aufgaben:** Anfragenbearbeitung, Vertragsauskünfte,
  Beschwerdemanagement, schriftliche Kundenkommunikation.
- **KI-Berührungspunkte:** Antwortentwürfe, Tonalitätsanpassung,
  Zusammenfassung von Vorgängen, Wissenssuche.
- **Besondere Anforderungen:** Datenschutz bei Kundendaten; kein ungeprüfter
  KI-Output direkt an Kundinnen und Kunden.

### 2.3 Makler und Vermittler

- **Typische Aufgaben:** Bedarfsermittlung, Tarifvergleich, Bestandspflege,
  Korrespondenz mit Versicherern und Kunden, Dokumentationspflichten.
- **KI-Berührungspunkte:** Bedingungsvergleich als Arbeitshilfe,
  Korrespondenzentwürfe, Aufbereitung von Unterlagen.
- **Besondere Anforderungen:** Haftungsrelevanz der Beratung — KI-Ergebnisse
  sind stets fachlich zu prüfen; Vergleichsergebnisse aus KI sind
  Arbeitsgrundlage, keine Empfehlung.

### 2.4 Underwriting

- **Typische Aufgaben:** Risikoprüfung, Annahmeentscheidungen, Tarifierung
  im Rahmen der Zeichnungsrichtlinien, Bestandsanalysen.
- **KI-Berührungspunkte:** Informationsaufbereitung, Extraktion aus
  Unterlagen, Plausibilisierung, Entwurfstexte für Rückfragen.
- **Besondere Anforderungen:** Annahme-, Pricing- und Zeichnungs-
  entscheidungen treffen Menschen. KI liefert Entscheidungsgrundlagen mit
  definiertem menschlichem Freigabepunkt. Hoher Bezug zum EU AI Act
  (Risikoklassifizierung entscheidungsnaher Systeme prüfen —
  REVIEW ERFORDERLICH: Regulatorik).

### 2.5 Schadenmanagement

- **Typische Aufgaben:** Schadenaufnahme, Deckungs- und Leistungsprüfung,
  Kommunikation mit Anspruchstellern und Dienstleistern, Betrugserkennung.
- **KI-Berührungspunkte:** Dokumentenauswertung, Zusammenfassungen,
  Korrespondenzentwürfe, Priorisierungsvorschläge.
- **Besondere Anforderungen:** Deckungs-/Leistungsentscheidungen und
  Betrugsverdacht niemals allein durch KI; jeder Verdachtshinweis ist ein
  Prüfauftrag an Menschen, kein Urteil.

### 2.6 Antrag und Betrieb

- **Typische Aufgaben:** Antragsbearbeitung, Vertragsänderungen,
  Bestandsführung, Datenpflege, Prozesssteuerung.
- **KI-Berührungspunkte:** Datenextraktion aus Anträgen, Prüfhinweise,
  Standardkorrespondenz, Prozessdokumentation.
- **Besondere Anforderungen:** Datenqualität und Nachvollziehbarkeit;
  automatisierte Verarbeitungsschritte brauchen definierte Kontrollpunkte.

### 2.7 Produktmanagement

- **Typische Aufgaben:** Produktentwicklung, Bedingungswerke, Markt- und
  Wettbewerbsanalysen, Anforderungsmanagement.
- **KI-Berührungspunkte:** Recherche, Analyse von Bedingungswerken,
  Entwurfsarbeit an Texten, Marktbeobachtung.
- **Besondere Anforderungen:** Produktfreigaben und POG-Prozesse
  (Product Oversight and Governance) bleiben menschlich verantwortet.

### 2.8 IT und Data

- **Typische Aufgaben:** Systemintegration, Datenarchitektur, Auswahl und
  Betrieb von KI-Werkzeugen, Schnittstellen, Automatisierung.
- **KI-Berührungspunkte:** Entwicklung und Betrieb von KI-Anwendungen,
  Datenpipelines, Evaluierung von Modellen und Anbietern.
- **Besondere Anforderungen:** Tiefere technische Inhalte als andere Rollen;
  zusätzlich Governance-Wissen (Modellrisiken, Auslagerung/Dienstleister-
  steuerung, IT-Sicherheitsanforderungen).

### 2.9 Compliance und Datenschutz

- **Typische Aufgaben:** Prüfung und Freigabe von KI-Einsätzen, Datenschutz-
  Folgenabschätzungen, Richtlinienarbeit, Schulung, Aufsichtskommunikation.
- **KI-Berührungspunkte:** Bewertung von KI-Anwendungsfällen, AI-Act- und
  DSGVO-Einordnung, Dokumentationsanforderungen.
- **Besondere Anforderungen:** Diese Rolle ist zugleich Zielgruppe und
  Review-Instanz für Akademie-Inhalte mit regulatorischem Bezug.

### 2.10 Management und Transformation

- **Typische Aufgaben:** Strategie, Priorisierung von KI-Initiativen,
  Organisations- und Kulturentwicklung, Budget- und Risikoentscheidungen.
- **KI-Berührungspunkte:** Use-Case-Bewertung, Governance-Aufbau,
  Befähigung der Organisation, Erfolgsmessung.
- **Besondere Anforderungen:** Überblickswissen statt Tooltiefe;
  realistische Einschätzung von Nutzen, Kosten, Risiken und Grenzen.

## 3. Vorwissen und Lernkontext

- **KI-Vorwissen:** heterogen — von „noch nie bewusst genutzt“ bis
  „täglich im Einsatz“. Lernpfade brauchen daher Einstiegsniveaus
  (Grundlagen / Anwendung / Vertiefung).
- **Zeitbudget:** Lernen findet überwiegend neben dem Tagesgeschäft statt.
  Einheiten müssen in 10–20 Minuten absolvierbar sein (Annahme, zu
  validieren).
- **Geräte:** Desktop im Büro, Smartphone unterwegs — mobile Nutzbarkeit
  ist Pflicht.
- **Sprache:** Deutsch. Schweiz- und österreichspezifische Abweichungen
  (Aufsicht, Datenschutzrecht) werden gekennzeichnet, wo relevant.

## 4. Abgrenzung

Nicht primäre Zielgruppe (Stand heute):

- Endkundinnen und Endkunden von Versicherungen
- Studierende ohne Branchenbezug (können Inhalte nutzen, sind aber nicht
  Maßstab für Didaktik und Beispiele)
- Reine KI-Forschung ohne Anwendungsbezug
