# Produktanforderungen (PRD) — MVP der VersicherungsTech KI-Akademie

**Status:** Entwurf zur Freigabe durch den Auftraggeber
**Stand:** 2026-07-14
**Grundlagen:** `CLAUDE.md`, `docs/project-vision.md`, `docs/target-groups.md`,
`docs/editorial-guidelines.md`, `docs/didactic-principles.md`,
`docs/security-and-privacy-rules.md`
**Ergänzende Dokumente:** `docs/user-stories.md`, `docs/mvp-scope.md`,
`docs/success-metrics.md`, `docs/acceptance-criteria.md`

Punkte, die eine Entscheidung des Auftraggebers benötigen, sind markiert mit
**`ENTSCHEIDUNG AUFTRAGGEBER`** und in Abschnitt 13 gesammelt.

---

## 1. Produktzusammenfassung

Die VersicherungsTech KI-Akademie ist eine textbasierte, videofreie
Lernplattform für die DACH-Versicherungsbranche. Der MVP liefert eine
öffentlich erreichbare Plattform mit einem vollständigen Pilotkurs
(„KI-Führerschein für den Versicherungsalltag“), Einstufungsassessment,
persönlichem Lernpfad, interaktiven Übungsformaten, Abschlussprüfung und
Nachweis. Geschäftsmodell ist ein **Freemium-Abo**: Einstieg kostenlos,
vollständiger Zugang per Premium-Abo.

### Bereits getroffene Entscheidungen des Auftraggebers

| Entscheidung | Inhalt |
|---|---|
| Geschäftsmodell | Freemium-Abo |
| Pilotkurs | Rollenunabhängiger Grundkurs „KI-Führerschein für den Versicherungsalltag“ |
| IDD | Keine Anrechnung als IDD-Weiterbildungszeit |
| Format | 100 % videofrei (Produktvorgabe, unverändert) |

## 2. Ziele des MVP

1. Nachweisen, dass die Zielgruppe ein textbasiertes, interaktives
   KI-Lernangebot annimmt und abschließt.
2. Den redaktionellen Produktions- und Review-Prozess (inkl.
   Regulatorik-Review) einmal vollständig durchlaufen.
3. Die Freemium-Mechanik validieren: Registrierungen aus der Landingpage,
   Conversion von Free zu Premium.
4. Eine technische und inhaltliche Basis schaffen, auf der rollenbezogene
   Lernpfade (Phase 2+) aufsetzen können, ohne Architekturbruch.

**Nicht-Ziele des MVP:** siehe `docs/mvp-scope.md` (u. a. keine
B2B-Mandantenfähigkeit, keine Community-Funktionen, keine rollenbezogenen
Vollpfade, keine Live-KI-Integration in Übungen — siehe Abschnitt 7.9).

## 3. Personas

Die Personas sind synthetisch und dienen der Produktentwicklung
(`SYNTHETISCHE DATEN`). Sie decken die Spannbreite der Rollen aus
`docs/target-groups.md` ab; der Pilotkurs ist bewusst rollenunabhängig.

### Persona 1 — „Die pragmatische Sachbearbeiterin“
- **Profil:** Sachbearbeitung Schaden bei einem mittelgroßen Versicherer,
  Mitte 40, 20 Jahre Berufserfahrung, KI bisher kaum genutzt.
- **Situation:** Ihr Arbeitgeber führt ein KI-Textwerkzeug ein; sie soll es
  nutzen, ist aber unsicher, was sie eingeben darf und wie sie Ergebnisse
  bewertet.
- **Bedürfnisse:** Klare Regeln („Was darf ich, was nicht?“), kleine
  Lerneinheiten neben dem Tagesgeschäft, kein Technikjargon.
- **Frust:** Schulungen, die mit Theorie beginnen; Angst, Fehler mit
  Kundendaten zu machen.
- **MVP-Relevanz:** Kernnutzerin des KI-Führerscheins; misst den Erfolg der
  Datenampel-Übungen und der verständlichen Sprache.

### Persona 2 — „Der effizienzgetriebene Makler“
- **Profil:** Selbstständiger Versicherungsmakler, Anfang 35, kleines Büro,
  nutzt privat bereits KI-Chatbots.
- **Situation:** Will KI für Korrespondenz und Unterlagenaufbereitung
  einsetzen, kennt aber weder Haftungs- noch Datenschutzgrenzen genau.
- **Bedürfnisse:** Sofort nutzbare Prompt-Vorlagen, mobile Nutzung zwischen
  Terminen, schnelle Antworten statt langer Kurse.
- **Frust:** Generische KI-Kurse ohne Versicherungsbezug; Zeitverschwendung.
- **MVP-Relevanz:** Prüft Prompt-Werkstatt, mobile Darstellung und die
  Freemium-Schwelle (zahlt nur bei klarem Nutzen).

### Persona 3 — „Die vorsichtige Führungskraft“
- **Profil:** Abteilungsleiterin Betrieb bei einem Versicherer, Ende 40,
  verantwortlich für 25 Mitarbeitende.
- **Situation:** Soll KI-Nutzung im Team ermöglichen, ohne Compliance-Risiken
  einzugehen; braucht selbst Grundverständnis, um Entscheidungen zu treffen.
- **Bedürfnisse:** Überblick über Chancen, Grenzen und Regulierung;
  Argumente und Regeln, die sie ins Team tragen kann; Nachweis, dass ihr
  Team geschult ist.
- **Frust:** Übertriebene KI-Versprechen; Unsicherheit, was der EU AI Act
  konkret für sie bedeutet.
- **MVP-Relevanz:** Prüft Modul 5 (Regulierung), Abschlussnachweis und ist
  Multiplikatorin für spätere B2B-Ausbaustufen.

### Persona 4 — „Der skeptische Underwriter“
- **Profil:** Underwriter Gewerbe bei einem Industrieversicherer, Anfang 50,
  fachlich sehr sicher, KI gegenüber skeptisch.
- **Situation:** Sieht KI-Ergebnisse von Kolleginnen und Kollegen und
  erkennt Fehler; will verstehen, wo KI ihm tatsächlich hilft und wo sie
  gefährlich ist.
- **Bedürfnisse:** Fachlich präzise Inhalte, ehrliche Darstellung von
  Fehlermodi, keine Werbesprache.
- **MVP-Relevanz:** Härtester Qualitätsmaßstab für Modul 3 (KI-Ergebnisse
  fachlich prüfen) und die Fallsimulationen; bricht bei Oberflächlichkeit ab.

### Persona 5 — „Die junge Kundenservice-Kraft“
- **Profil:** Kundenservice bei einem InsurTech, Mitte 20, digital versiert,
  nutzt KI täglich — teils ohne Freigabe („Schatten-KI“).
- **Situation:** Nutzt private KI-Tools für Arbeitsaufgaben, ohne Risiken zu
  kennen; ihr Arbeitgeber hat noch keine klaren Regeln.
- **Bedürfnisse:** Schnelle, mobile Lerneinheiten; konkrete Do's und
  Don'ts; kein belehrender Ton.
- **MVP-Relevanz:** Testet mobile Nutzung, kurze Einheiten und ob die
  Sicherheitsinhalte auch Vielnutzer erreichen (nicht nur Einsteiger).

## 4. Jobs to be Done (JTBD)

| # | Wenn ich … (Situation) | … möchte ich … (Motivation) | … damit … (Ergebnis) |
|---|---|---|---|
| J1 | zum ersten Mal beruflich mit KI arbeiten soll | verstehen, was KI kann und was nicht — ohne Techniknebel | ich Werkzeuge realistisch einschätze und Vertrauen aufbaue |
| J2 | eine Aufgabe mit einem KI-Tool erledigen will | wissen, wie ich sie richtig formuliere (prompte) | ich brauchbare Ergebnisse in weniger Zeit bekomme |
| J3 | ein KI-Ergebnis vor mir habe | erkennen, ob es fachlich stimmt und wo ich prüfen muss | ich keine Fehler an Kunden oder in Akten weitergebe |
| J4 | unsicher bin, welche Daten ich eingeben darf | eine klare, schnelle Entscheidungshilfe haben | ich keinen Datenschutzverstoß begehe |
| J5 | von Regulierung (AI Act, DSGVO) höre | wissen, was davon mich im Alltag konkret betrifft | ich handlungsfähig bin, ohne Jurist sein zu müssen |
| J6 | KI regelmäßig nutzen will | aus Einzel-Prompts einen sicheren Arbeitsablauf machen | KI-Nutzung zuverlässig, wiederholbar und geprüft ist |
| J7 | eine Weiterbildung abgeschlossen habe | einen vorzeigbaren Nachweis erhalten | ich meine Kompetenz gegenüber Arbeitgeber/Kunden belegen kann |
| J8 | wenig Zeit habe | in 10–20-Minuten-Einheiten lernen, auch mobil | Lernen neben dem Tagesgeschäft realistisch stattfindet |
| J9 | als Führungskraft mein Team befähigen soll | seriöse, geprüfte Inhalte mit Quellen finden | ich sie guten Gewissens weiterempfehlen kann |
| J10 | nach etwas Bestimmtem suche (z. B. „Datenampel“) | Inhalte gezielt finden statt Kurse zu durchblättern | die Plattform auch als Nachschlagewerk funktioniert |

## 5. Nutzerrollen (Systemrollen)

| Rolle | Beschreibung | Rechte (Kurzfassung) |
|---|---|---|
| **Gast** | Nicht eingeloggte Besucherin | Landingpage, Kurskatalog, Kursvorschau, frei geschaltete Inhalte lesen; Registrierung |
| **Lernende/r (Free)** | Registriert, kein Abo | Frei geschaltete Module vollständig nutzen, Einstufungsassessment, Lernfortschritt, persönlicher Lernpfad (mit Premium-Hinweisen) |
| **Lernende/r (Premium)** | Aktives Abo | Alle Kursinhalte, Abschlussprüfung, Badges/Zertifikat, alle Übungsformate |
| **Autor/in (Redaktion)** | Erstellt und pflegt Inhalte | Inhalte anlegen/ändern im Entwurfsstatus, Quellen und Rechtsstand pflegen |
| **Reviewer/in** | Fach- und Regulatorik-Review | Review-Status setzen (insb. `REVIEW ERFORDERLICH: Regulatorik` auflösen), Freigabe oder Rückweisung mit Kommentar |
| **Admin** | Betrieb der Plattform | Nutzerverwaltung, Abo-Verwaltung, Veröffentlichung, Konfiguration |

Hinweis: Autor/Reviewer/Admin arbeiten im MVP ggf. ohne eigenes UI direkt am
Content-Repository (Git-basierter Workflow) — siehe `docs/mvp-scope.md`,
Entscheidung E5.

## 6. Freemium-Modell

**Vorschlag** (— **ENTSCHEIDUNG AUFTRAGGEBER**, siehe Abschnitt 13, E1):

| Kostenlos (Free) | Premium-Abo |
|---|---|
| Landingpage, Kurskatalog, Suche | Alle Module des Kurses (2–7) |
| Einstufungsassessment + persönlicher Lernpfad | Alle Fallsimulationen und Übungen |
| Modul 1 des KI-Führerscheins vollständig | Abschlussprüfung |
| Je Modul: Vorschau (Nutzenversprechen + Gliederung) | Badges und Zertifikatsnachweis |
| Lernfortschritt für freie Inhalte | Lernfortschritt vollständig |

Begründung des Vorschlags: Das Assessment und Modul 1 zeigen den Wert der
Plattform und erzeugen einen persönlichen Lernpfad, dessen Fortsetzung hinter
der Premium-Schwelle liegt — ein natürlicher, nicht aggressiver
Conversion-Punkt.

Preis, Laufzeiten (monatlich/jährlich) und Zahlungsanbieter:
**ENTSCHEIDUNG AUFTRAGGEBER** (E2). Für den MVP ist auch ein Start ohne
Bezahlstrecke möglich (Premium per manueller Freischaltung/Warteliste), um
die Bezahlintegration zu entkoppeln (E2a).

## 7. Funktionale Anforderungen

Nummerierung `FR-x.y`. Detaillierte User Stories: `docs/user-stories.md`;
Akzeptanzkriterien: `docs/acceptance-criteria.md`.

### 7.1 Öffentliche Landingpage (FR-1)

- FR-1.1 Öffentliche Startseite mit Nutzenversprechen der Akademie,
  Zielgruppenbezug (DACH-Versicherungsbranche) und Einstieg in Kurskatalog
  und Registrierung.
- FR-1.2 Vorstellung des Pilotkurses mit Modulübersicht.
- FR-1.3 Klare Darstellung des Freemium-Modells (was ist frei, was Premium).
- FR-1.4 Rechtspflichtseiten: Impressum, Datenschutzerklärung,
  ggf. AGB für das Abo (Inhalte liefert Auftraggeber — E3).
- FR-1.5 Tonalität und Inhalte gemäß `docs/editorial-guidelines.md`;
  keine Marketingfloskeln, keine „KI-konform“-Versprechen.

### 7.2 Kurskatalog (FR-2)

- FR-2.1 Übersicht aller veröffentlichten Kurse (MVP: einer) mit Titel,
  Kurzbeschreibung, Modulanzahl, geschätzter Lernzeit, Niveau und
  Free/Premium-Kennzeichnung.
- FR-2.2 Kursdetailseite mit Modulliste, Lernzielen, Formaten und
  Quellen-/Versionsangaben (siehe FR-13).
- FR-2.3 **Rollenbezogene Filter:** Inhalte sind mit Rollen aus
  `docs/target-groups.md` verschlagwortet; der Katalog ist nach Rolle
  filterbar. Im MVP filtert dies Module/Lektionen mit besonderem
  Rollenbezug (z. B. rollenspezifische Beispiele), da der Pilotkurs
  rollenunabhängig ist. Das Filterkonzept ist auf spätere Rollenpfade
  ausgelegt.
- FR-2.4 Filter nach Niveau (Grundlagen/Anwendung/Vertiefung) und Format
  vorbereitet (Taxonomie im Content-Modell), UI im MVP mindestens für
  Rolle und Niveau.

### 7.3 Einstufungsassessment (FR-3)

- FR-3.1 Freiwilliges Assessment (ca. 10–15 Fragen) zu Vorwissen,
  Rolle, KI-Nutzungserfahrung und Selbsteinschätzung.
- FR-3.2 Fragetypen: Single/Multiple Choice und Selbsteinschätzungsskalen;
  vollständig text-/formularbasiert.
- FR-3.3 Ergebnis: Einstufung (z. B. Einsteiger / Anwender / Fortgeschritten)
  mit verständlicher Begründung — ausdrücklich als Lernempfehlung, nicht als
  Leistungsbewertung formuliert.
- FR-3.4 Ergebnis erzeugt den persönlichen Lernpfad (FR-4).
- FR-3.5 Assessment ist wiederholbar; das letzte Ergebnis zählt.
- FR-3.6 Ohne Assessment ist der Standard-Lernpfad (alle Module in
  Reihenfolge) nutzbar — das Assessment ist Empfehlung, keine Pflicht.

### 7.4 Persönlicher Lernpfad (FR-4)

- FR-4.1 Aus Assessment (Rolle, Niveau, Vorerfahrung) wird eine persönliche
  Reihenfolge und Gewichtung der Module/Lektionen erzeugt (z. B. Einsteiger:
  alle Module linear; Fortgeschrittene: Modul 1 als optionale Auffrischung
  markiert).
- FR-4.2 Der Lernpfad zeigt: nächste empfohlene Einheit, Fortschritt,
  verbleibende geschätzte Lernzeit.
- FR-4.3 Rollenbezug: Wo Lektionen rollenspezifische Beispiele/Varianten
  haben, zeigt der Lernpfad bevorzugt die zur angegebenen Rolle passenden.
- FR-4.4 Lernende können vom Pfad abweichen (freie Navigation); der Pfad
  ist Empfehlung, keine Sperre — mit Ausnahme der Abschlussprüfung (FR-11.2).
- FR-4.5 Premium-Inhalte sind im Pfad sichtbar, aber für Free-Nutzer als
  Premium gekennzeichnet (Conversion-Punkt, kein Dark Pattern:
  klare, ehrliche Kennzeichnung).

### 7.5 Textbasierte Lektionen (FR-5)

- FR-5.1 Lektionen folgen der Struktur aus `docs/editorial-guidelines.md`
  (Nutzenversprechen → Kerninhalt → Praxisteil → Grenzen & Kontrolle →
  Zusammenfassung → Transferaufgabe).
- FR-5.2 Unterstützte Inhaltselemente: Überschriften, Absätze, Listen,
  Tabellen, annotierte Beispiele (Text mit Randkommentaren), Hinweisboxen
  (u. a. für Pflicht-Marker wie `SYNTHETISCHE DATEN`), Checklisten,
  Prozesskarten (als strukturierte Text-/Grafikdarstellung mit
  Textalternative), Zitate mit Quellenangabe.
- FR-5.3 Lesezeit-Schätzung je Lektion sichtbar.
- FR-5.4 Kein Video- oder Audio-Element im Content-Modell — das
  Inhaltsformat sieht solche Typen bewusst nicht vor.
- FR-5.5 Lektionen sind einzeln verlinkbar (stabile URLs) für
  Nachschlage-Nutzung und Suche.

### 7.6 Quizze (FR-6)

- FR-6.1 Fragetypen im MVP: Single Choice, Multiple Choice,
  Richtig/Falsch, Zuordnung (Matching).
- FR-6.2 **Jede** Antwortoption hat erklärendes Feedback — auch richtige
  („richtig, weil …“), gemäß `docs/didactic-principles.md`.
- FR-6.3 Quizze innerhalb von Lektionen (formativ, beliebig wiederholbar,
  keine Bewertung gespeichert außer „bearbeitet“) und am Modulende
  (Modul-Check, Ergebnis fließt in Fortschritt ein).
- FR-6.4 Quizfragen sind im Content-Modell deklarativ definiert (Daten,
  nicht Code), damit die Redaktion sie ohne Entwickler pflegen kann.

### 7.7 Verzweigte Fallsimulationen (FR-7)

- FR-7.1 Textbasierte Szenarien mit Entscheidungspunkten; jede Entscheidung
  führt zu einem anderen Fortgang (Baumstruktur, im MVP 2–4 Ebenen).
- FR-7.2 Jeder Pfad endet mit einer Auswertung: getroffene Entscheidungen,
  Konsequenzen, was ein sicherer Umgang gewesen wäre — fehlerfreundlich
  formuliert (sicherer Übungsraum).
- FR-7.3 Simulationen verwenden ausschließlich synthetische Fälle mit
  Kennzeichnung `SYNTHETISCHE DATEN`.
- FR-7.4 In entscheidungsnahen Szenarien (z. B. Abschlussfall) ist der
  menschliche Kontrollpunkt Teil der Simulation: Es gibt Pfade, in denen
  „KI-Ergebnis ungeprüft übernehmen“ als Fehlentscheidung erlebbar wird.
- FR-7.5 Simulationen sind wiederholbar; alle Pfade bleiben erkundbar
  („Andere Entscheidung ausprobieren“).
- FR-7.6 Deklaratives Format im Content-Modell (Knoten, Kanten, Feedback als
  Daten).

### 7.8 Datenampel-Übungen (FR-8)

Die „Datenampel“ ist das zentrale Übungsformat für Modul 4: Lernende ordnen
Datenarten oder konkrete (synthetische) Eingabe-Situationen einer Ampel zu:

- **Grün:** darf in ein freigegebenes KI-Tool eingegeben werden.
- **Gelb:** nur unter Bedingungen (z. B. nach Entfernen von Personenbezug,
  nur in intern freigegebenen Tools) — Bedingung muss benannt werden.
- **Rot:** darf nicht eingegeben werden.

Anforderungen:

- FR-8.1 Übungstyp „Ampel-Zuordnung“: Item (z. B. „Schadenschilderung mit
  Namen und Geburtsdatum des Kunden“) per Auswahl auf Grün/Gelb/Rot legen.
- FR-8.2 Erklärendes Feedback je Item, inkl. der Begründung (z. B.
  Personenbezug, Gesundheitsdaten, Geschäftsgeheimnis) und des sicheren
  Alternativvorgehens.
- FR-8.3 Deutlicher Hinweis in jeder Übung: Die Ampel ist ein
  **Lernmodell**; verbindlich sind immer die internen Richtlinien des
  eigenen Unternehmens. Keine „damit sind Sie DSGVO-konform“-Aussagen.
- FR-8.4 Items sind synthetisch und im Content-Modell deklarativ gepflegt.
- FR-8.5 Barrierefrei bedienbar (Auswahl statt reiner Drag-and-drop-Pflicht;
  Ampelfarben immer mit Textlabel, nie Farbe allein).

### 7.9 Prompt-Werkstatt (FR-9)

- FR-9.1 Bibliothek kommentierter Prompt-Vorlagen für typische
  Versicherungsaufgaben (Korrespondenz-Entwurf, Zusammenfassung,
  Strukturierung von Unterlagen …), je Vorlage: Einsatzzweck, Grenzen,
  Prüfschritte, Rollen-Tags.
- FR-9.2 Interaktiver Prompt-Bausatz: Lernende bauen aus Bausteinen
  (Rolle/Kontext, Aufgabe, Eingabedaten, Format, Prüfauftrag) einen Prompt
  zusammen; die Übung gibt regelbasiertes Feedback zur Struktur (z. B.
  „Kontext fehlt“, „Eingabedaten enthalten rote Ampel-Daten“).
- FR-9.3 Kopierfunktion für fertige Prompts zur Nutzung im eigenen,
  intern freigegebenen KI-Tool — mit stehendem Sicherheitshinweis
  (keine realen Kundendaten, Ergebnis fachlich prüfen).
- FR-9.4 **MVP ohne Live-LLM-Anbindung:** Das Feedback der Werkstatt ist
  regelbasiert/vordefiniert; es wird kein KI-Modell aus der Plattform heraus
  aufgerufen. Begründung: offene Datenschutz- und Kostenfragen (L3 in
  `docs/open-questions.md`); die Übungen funktionieren didaktisch auch so,
  praktische Tool-Aufgaben verweisen auf das eigene freigegebene Tool der
  Lernenden. Live-Anbindung als Ausbaustufe — **ENTSCHEIDUNG AUFTRAGGEBER**
  (E4), falls sie doch in den MVP soll.

### 7.10 Lernfortschritt (FR-10)

- FR-10.1 Je Lektion/Übung/Simulation wird der Status gespeichert:
  offen / begonnen / abgeschlossen.
- FR-10.2 Fortschritt je Modul und für den Kurs gesamt (Prozent, absolvierte
  Einheiten, geschätzte Restzeit) auf einer persönlichen Übersichtsseite.
- FR-10.3 „Weiterlernen“-Einstieg: Ein Klick führt zur nächsten offenen
  Einheit des Lernpfads.
- FR-10.4 Fortschritt ist geräteübergreifend (an den Account gebunden).
- FR-10.5 Datensparsamkeit: gespeichert werden nur Status und
  Modul-/Prüfungsergebnisse; keine Detailprotokolle einzelner Antworten
  über das didaktisch Nötige hinaus (siehe NFR-D und
  `docs/security-and-privacy-rules.md`).

### 7.11 Abschlussprüfung (FR-11)

- FR-11.1 Kursweite Abschlussprüfung: Mischung aus Quizfragen und einer
  verzweigten Prüfungssimulation auf Basis von Modul 7 („Ein Vorgang, fünf
  Risiken“).
- FR-11.2 Zulassung: alle Module abgeschlossen (Premium erforderlich).
- FR-11.3 Bestehensgrenze: Vorschlag 80 % der Punkte, alle fünf
  „Risiko-Situationen“ des Abschlussfalls müssen sicher gelöst sein —
  Bestehensgrenze final: **ENTSCHEIDUNG AUFTRAGGEBER** (E6).
- FR-11.4 Bei Nichtbestehen: erklärendes Feedback nach Themenfeldern und
  Wiederholung möglich (Vorschlag: nach frühestens 24 Stunden, unbegrenzte
  Versuche — E6).
- FR-11.5 Prüfungsfragen werden aus einem Fragenpool variiert (Reihenfolge
  und Auswahl), um reines Auswendiglernen zu erschweren.
- FR-11.6 Klarer Hinweis, dass der Nachweis eine Weiterbildungsbestätigung
  der Akademie ist — kein amtliches Zertifikat, keine IDD-Zeit.

### 7.12 Badges und Zertifikatsnachweis (FR-12)

- FR-12.1 **Badge je Modul** bei Abschluss (Modul-Check bestanden).
- FR-12.2 **Kurszertifikat** („KI-Führerschein für den Versicherungsalltag“)
  als PDF nach bestandener Abschlussprüfung: Name der/des Lernenden,
  Kurs, Datum, Version des Kurses (Rechtsstand-Bezug), Aussteller
  VersicherungsTech KI-Akademie.
- FR-12.3 Zertifikat per stabiler URL/Code verifizierbar (Echtheitsprüfung
  ohne Login) — Vorschlag, Umfang im MVP: **ENTSCHEIDUNG AUFTRAGGEBER** (E7).
- FR-12.4 Keine Konformitäts- oder Kompetenzgarantien im Zertifikatstext;
  Formulierung reviewpflichtig (`REVIEW ERFORDERLICH: Regulatorik` für den
  Zertifikatstext).

### 7.13 Quellen- und Versionsangaben (FR-13)

- FR-13.1 Jede Lektion zeigt: Version, Datum der letzten inhaltlichen
  Änderung, `RECHTSSTAND: JJJJ-MM-TT` (wo regulatorische Aussagen enthalten
  sind) und Quellenverzeichnis mit Fundstellen.
- FR-13.2 Quellen sind als strukturierte Daten am Inhalt gepflegt (nicht nur
  Fließtext), damit sie prüfbar und filterbar sind.
- FR-13.3 Nicht verifizierte Quellen tragen sichtbar
  `QUELLE ZU VERIFIZIEREN` — solche Inhalte können nicht auf Status
  „veröffentlicht“ gesetzt werden (siehe FR-14).
- FR-13.4 Änderungshistorie je Lektion mindestens intern nachvollziehbar
  (Versionierung im Content-Repository); sichtbare „Was ist neu“-Anzeige für
  Lernende ist Ausbaustufe.

### 7.14 Redaktioneller Review-Status (FR-14)

- FR-14.1 Jeder Inhalt hat einen Workflow-Status:
  `Entwurf` → `Fachreview` → `Regulatorik-Review` (nur wenn Marker gesetzt)
  → `Freigegeben` → `Veröffentlicht`; zusätzlich `Zurückgezogen`.
- FR-14.2 Nur Inhalte im Status `Veröffentlicht` sind für Lernende sichtbar.
- FR-14.3 Inhalte mit Marker `REVIEW ERFORDERLICH: Regulatorik` können
  `Veröffentlicht` nur über den Zwischenschritt Regulatorik-Review erreichen;
  das System erzwingt dies (kein manuelles Überspringen).
- FR-14.4 Review-Entscheidungen (wer, wann, Ergebnis, Kommentar) werden
  dokumentiert.
- FR-14.5 Umsetzung im MVP wahrscheinlich Git-basiert (Status als Metadatum,
  Review per Pull Request) statt eigener Redaktions-UI —
  Architekturentscheidung per ADR in Phase 2 (E5).

### 7.15 Suchfunktion (FR-15)

- FR-15.1 Volltextsuche über alle veröffentlichten Inhalte (Lektionen,
  Prompt-Vorlagen, Checklisten, Glossarbegriffe).
- FR-15.2 Suchergebnisse mit Titel, Inhaltstyp, Modul-/Kurszuordnung,
  Textauszug (Snippet) und Free/Premium-Kennzeichnung.
- FR-15.3 Filter der Suche nach Rolle und Inhaltstyp.
- FR-15.4 Premium-Inhalte erscheinen in der Suche für Free-Nutzer mit
  Titel/Snippet und Premium-Kennzeichnung (Auffindbarkeit ja, Volltext nein).

### 7.16 Konto, Registrierung und Abo (FR-16)

- FR-16.1 Registrierung mit E-Mail und Passwort inkl.
  E-Mail-Verifizierung; Double-Opt-in für jede werbliche Kommunikation.
- FR-16.2 Profil: Anzeigename, Rolle (aus Rollenliste, freiwillig),
  Organisationstyp (freiwillig) — beides steuert Filter/Lernpfad.
- FR-16.3 Passwort-Reset per E-Mail.
- FR-16.4 Abo-Verwaltung: Premium abschließen, kündigen, Status einsehen.
  Umsetzung abhängig von E2/E2a (Zahlungsanbieter oder manuelle
  Freischaltung im MVP).
- FR-16.5 Konto löschen: Selbstbedienung; löscht personenbezogene Daten
  gemäß Löschkonzept (L2 in `docs/open-questions.md` — vor Implementierung
  zu klären).
- FR-16.6 Datenauskunft/-export mindestens auf Anfrage (organisatorischer
  Prozess genügt im MVP).

## 8. Nichtfunktionale Anforderungen

### NFR-A Barrierefreiheit
- NFR-A1 Orientierung an WCAG 2.1 AA für alle Lernenden-Flächen.
- NFR-A2 Vollständige Tastaturbedienbarkeit aller Interaktionen (Quiz,
  Simulation, Datenampel, Prompt-Bausatz).
- NFR-A3 Screenreader-Tauglichkeit: semantisches HTML, Landmarken, Labels,
  sinnvolle Fokusreihenfolge, Statusmeldungen (z. B. Quiz-Feedback) als
  Live-Region.
- NFR-A4 Keine Information nur über Farbe (insb. Datenampel: immer
  Textlabel), Kontrast mindestens 4,5:1 für Fließtext.
- NFR-A5 Skalierbarkeit: Layout bleibt bei 200 % Textzoom nutzbar.

### NFR-B Mobile Nutzung
- NFR-B1 Responsives Design; alle Kernflows (Lernen, Quiz, Simulation,
  Suche, Fortschritt) auf Smartphone-Viewports (ab 360 px Breite) voll
  nutzbar.
- NFR-B2 Touch-Ziele ausreichend groß; keine Hover-abhängigen Funktionen.
- NFR-B3 Lesbarkeit: Zeilenlänge und Typografie für längere Texte auf
  kleinen Bildschirmen optimiert.

### NFR-C Performance
- NFR-C1 Inhaltsseiten laden auf mobiler Mittelklasse-Hardware und 4G in
  unter ~3 Sekunden bis zur Interaktivität (Richtwert; Messmethode in
  Phase 2 festlegen).
- NFR-C2 Textbasierte Inhalte werden so ausgeliefert, dass sie auch bei
  schwacher Verbindung nutzbar sind (kleine Seitengewichte; das videofreie
  Konzept unterstützt das).

### NFR-D Datenschutz und Sicherheit
- NFR-D1 Verbindlich: alle Regeln aus `docs/security-and-privacy-rules.md`
  (Datensparsamkeit, Zweckbindung, keine Secrets im Repo, synthetische
  Daten, AV-Verträge, EU-Hosting-Präferenz — T5/L2/L3 offen).
- NFR-D2 Transportverschlüsselung (HTTPS) überall; Passwörter nach Stand der
  Technik gehasht.
- NFR-D3 Kein Tracking ohne Rechtsgrundlage; Analytik datensparsam (T6).
- NFR-D4 Lernstandsdaten sind nicht für Dritte (z. B. Arbeitgeber) einsehbar;
  eine solche Funktion existiert im MVP nicht.

### NFR-E Wartbarkeit und Redaktionsfähigkeit
- NFR-E1 Strikte Trennung Inhalt/Präsentation/Logik; alle Lernformate
  (Quiz, Simulation, Ampel, Prompt-Bausatz) deklarativ im Content-Modell.
- NFR-E2 Redaktion kann Inhalte ohne Code-Änderung erstellen und ändern
  (Git-Workflow zulässig, aber ohne Programmierkenntnis-Pflicht anstreben).
- NFR-E3 Inhalte versioniert; jede Veröffentlichung reproduzierbar.
- NFR-E4 Automatisierte Prüfungen im Content-Build: Pflichtfelder (Version,
  Status, Quellen bei Regulatorik-Marker), keine verbotenen Inhaltstypen
  (Video), Marker-Konsistenz (z. B. `QUELLE ZU VERIFIZIEREN` blockiert
  Veröffentlichung).
- NFR-E5 Code getestet und dokumentiert gemäß `docs/definition-of-done.md`;
  Architekturentscheidungen als ADR.

### NFR-F Verfügbarkeit und Betrieb
- NFR-F1 MVP-Ziel: „Werktags zuverlässig nutzbar“; formale SLOs erst mit
  Betriebsmodell (Phase 2). Kein 24/7-Support im MVP.
- NFR-F2 Regelmäßige Backups der Nutzer- und Fortschrittsdaten;
  Wiederherstellung getestet.
- NFR-F3 Kein Deployment ohne ausdrückliche Freigabe des Auftraggebers.

## 9. Kern-User-Flows

### Flow 1 — Entdecken und Registrieren (Gast → Free)
1. Gast landet auf der Landingpage (Suche, Empfehlung, Magazin-Verweis).
2. Liest Nutzenversprechen, öffnet Kurskatalog, sieht Kursdetailseite des
   KI-Führerscheins mit Modulübersicht und Free/Premium-Kennzeichnung.
3. Startet Modul-1-Vorschau oder direkt die Registrierung.
4. Registriert sich (E-Mail, Passwort, Verifizierung), gibt optional Rolle an.
5. Landet auf „Mein Lernbereich“ mit Empfehlung: Einstufungsassessment.

### Flow 2 — Einstufung und persönlicher Lernpfad (Free)
1. Lernende startet das Assessment (10–15 Fragen, ca. 5–10 Minuten).
2. Erhält Einstufung mit Begründung und den persönlichen Lernpfad.
3. Pfad zeigt Modul 1 (frei) als ersten Schritt; Module 2–7 sichtbar mit
   Premium-Kennzeichnung.
4. Beginnt Modul 1 direkt aus dem Pfad.

### Flow 3 — Lernen einer Einheit (Free/Premium)
1. „Weiterlernen“ führt zur nächsten offenen Einheit.
2. Lektion: Nutzenversprechen → Kerninhalt mit annotierten Beispielen →
   eingebettetes Kurzquiz mit erklärendem Feedback → Grenzen & Kontrolle →
   Zusammenfassung → Transferaufgabe.
3. Einheit wird als abgeschlossen markiert; Fortschritt aktualisiert sich;
   nächste Einheit wird angeboten.

### Flow 4 — Free → Premium (Conversion)
1. Free-Nutzerin schließt Modul 1 ab; Lernpfad zeigt Modul 2 mit
   Premium-Hinweis.
2. Klick auf „Premium freischalten“ → transparente Abo-Seite
   (Leistungen, Preis, Kündigung).
3. Abschluss (Zahlungsanbieter oder manuelle Freischaltung je nach E2a).
4. Zurück in den Lernpfad; Modul 2 startet ohne Umwege.

### Flow 5 — Fallsimulation und Datenampel (Premium)
1. In Modul 4 öffnet die Lernende eine Datenampel-Übung; ordnet 8–12
   synthetische Situationen zu; erhält je Item Feedback mit Begründung.
2. In der anschließenden Fallsimulation trifft sie Entscheidungen in einem
   verzweigten Szenario; ein Pfad enthält den Fehler „ungeprüft übernehmen“
   und macht die Konsequenz erlebbar.
3. Auswertung mit Empfehlung, welche Lektion bei Unsicherheit wiederholt
   werden sollte.

### Flow 6 — Abschlussprüfung und Zertifikat (Premium)
1. Alle Module abgeschlossen → Abschlussprüfung wird im Lernpfad
   freigeschaltet; Hinweis auf Ablauf, Dauer und Bestehensgrenze.
2. Prüfung: Fragenpool-Quiz + Prüfungssimulation „Ein Vorgang, fünf Risiken“.
3. Bestanden: Badge „Kurs abgeschlossen“, PDF-Zertifikat zum Download,
   optional Verifizierungslink. Nicht bestanden: Auswertung nach
   Themenfeldern, Wiederholung nach Frist.

### Flow 7 — Suchen und Nachschlagen (alle Rollen)
1. Nutzerin sucht z. B. „Gesundheitsdaten Prompt“.
2. Ergebnisliste mit Typ, Snippet, Rolle-Tags, Free/Premium-Kennzeichnung.
3. Öffnet Checkliste oder Lektion direkt (stabile URL); Gast wird bei
   Premium-Inhalt zur Registrierung/Abo-Seite geführt.

### Flow 8 — Redaktioneller Review (Redaktion, intern)
1. Autor/in erstellt Lektion im Status `Entwurf`, pflegt Quellen, Version,
   Rechtsstand und Marker.
2. Fachreview prüft, kommentiert, gibt frei oder weist zurück.
3. Bei Regulatorik-Marker: zusätzliches Regulatorik-Review; ohne dessen
   Freigabe keine Veröffentlichung (systemseitig erzwungen).
4. Freigegebener Inhalt wird veröffentlicht; Version und Datum erscheinen
   am Inhalt.

## 10. Pilotkurs: „KI-Führerschein für den Versicherungsalltag“

Rollenunabhängiger Grundkurs (Niveau: Grundlagen/Anwendung). Zielumfang je
Modul: 3–5 Lerneinheiten à 10–20 Minuten. Die folgende Struktur ist die
inhaltliche Anforderung an die Kursproduktion (Phase 3) — noch keine
Kursinhalte.

| # | Modul | Kern-Lernziele | Prägende Formate |
|---|---|---|---|
| 1 | **KI verstehen – ohne Techniknebel** | Was generative KI ist und was nicht; realistische Stärken/Schwächen; typische Fehlermodi (Halluzination, veraltetes Wissen, Bias) an Versicherungsbeispielen | Lektionen, annotierte Beispiele, Quiz |
| 2 | **Sicher prompten im Versicherungsalltag** | Prompt-Aufbau (Kontext, Aufgabe, Daten, Format, Prüfauftrag); typische Alltagsaufgaben; Grenzen | Lektionen, Prompt-Werkstatt, Prompt-Vorlagen |
| 3 | **KI-Ergebnisse fachlich prüfen** | Prüfstrategien; Halluzinationen und Plausibilitätsfehler erkennen; Vier-Augen-Prinzip Mensch/KI | Annotierte Beispiele („Finde die Fehler im KI-Output“), interaktive Dokumentenübung, Quiz |
| 4 | **Kundendaten sicher verwenden** | Personenbezug erkennen; besondere Kategorien (Gesundheitsdaten); Datenampel anwenden; sichere Alternativen | Datenampel-Übungen, Checkliste, Fallsimulation |
| 5 | **Regulierung und verantwortungsvoller Einsatz** | Überblick EU AI Act und DSGVO im Arbeitsalltag; menschliche Kontrollpunkte; interne Richtlinien; Grenzen der eigenen Verantwortung — `REVIEW ERFORDERLICH: Regulatorik` | Lektionen mit Quellen + Rechtsstand, Entscheidungsbaum („Darf ich KI hier einsetzen?“), Quiz |
| 6 | **Vom Prompt zum sicheren Arbeitsablauf** | Aus Einzel-Prompts wiederholbare Abläufe machen; Prozesskarte mit KI- und Kontrollpunkten; Dokumentation | Prozesskarten, Transferaufgabe, schriftliches Rollenspiel |
| 7 | **Abschlussfall: Ein Vorgang, fünf Risiken** | Anwendung von allem: ein synthetischer Vorgang durchläuft fünf Risikosituationen (Dateneingabe, Halluzination, Regulatorik, fehlender Kontrollpunkt, Kommunikation) | Große verzweigte Fallsimulation; Basis der Abschlussprüfung |

Kursproduktion unterliegt vollständig `docs/editorial-guidelines.md`,
`docs/didactic-principles.md` und `docs/security-and-privacy-rules.md`
(inkl. DoD je Einheit).

## 11. MVP-Abgrenzung und Ausbaustufen

Verbindliche In/Out-Liste und Phasenplanung: `docs/mvp-scope.md`.

## 12. Risiken

| # | Risiko | Auswirkung | Gegenmaßnahme |
|---|---|---|---|
| R1 | Freemium-Schwelle falsch gesetzt: zu viel frei (keine Conversion) oder zu wenig (kein Einstieg) | Geschäftsmodell scheitert | Klarer Vorschlag (Modul 1 + Assessment frei), Messung ab Tag 1, Schwelle bewusst änderbar bauen |
| R2 | Interaktive Formate (Simulation, Ampel, Prompt-Bausatz) technisch unterschätzt | Verzögerung, Qualitätsverlust | Deklaratives Content-Modell zuerst entwerfen (ADR), Formate einzeln pilotieren, notfalls Formatumfang im MVP reduzieren (Priorität siehe `docs/mvp-scope.md`) |
| R3 | Regulatorik-Inhalte (Modul 5) veralten oder enthalten Fehler | Reputations- und Haftungsrisiko | Erzwungener Review-Workflow (FR-14.3), Rechtsstand-Anzeige, Review-Intervall (D6), „keine Rechtsberatung“-Hinweis (L4) |
| R4 | Review-Engpass: Fach-/Regulatorik-Reviewer nicht besetzt (R1/R2 in open-questions) | Kursproduktion blockiert | Personen vor Produktionsstart benennen — ENTSCHEIDUNG AUFTRAGGEBER (E8) |
| R5 | Prüfungs-/Zertifikatslogik weckt falsche Erwartungen (amtlicher Nachweis) | Vertrauensverlust, rechtliche Angriffsfläche | Klare Formulierungen (FR-11.6, FR-12.4), Zertifikatstext reviewpflichtig |
| R6 | Bezahlstrecke verzögert den MVP | Später Marktstart | Entkopplung möglich: Start mit manueller Premium-Freischaltung (E2a) |
| R7 | Ein einzelner rollenunabhängiger Kurs wirkt für Spezialisten (z. B. Underwriting) zu flach | Zielgruppenteile springen ab | Rollenspezifische Beispiele/Varianten in Lektionen (FR-4.3), Vertiefungspfade als klar kommunizierte Ausbaustufe |
| R8 | Datenschutz-Grundsatzfragen (Hosting, Löschfristen, Analytics — T5/L2/T6) verschleppen sich bis in die Implementierung | Umbauten, rechtliches Risiko | Klärung als Blocker vor Implementierungsstart einplanen (siehe `docs/mvp-scope.md`, Voraussetzungen) |
| R9 | Akzeptanz des videofreien Formats geringer als angenommen (A6) | Kernannahme wackelt | Früh mit Pilotnutzern testen; Textstärken (Suche, Tempo, Nachschlagen) im UI erlebbar machen |
| R10 | Suchfunktion schwach → Plattform funktioniert nicht als Nachschlagewerk (J10) | Wiederkehr-Nutzung sinkt | Suche als Kernfeature behandeln, nicht als Beiwerk; Qualität in Akzeptanzkriterien verankert |

## 13. Entscheidungsbedarf des Auftraggebers (gesammelt)

| # | Entscheidung | Kontext | Vorschlag |
|---|---|---|---|
| E1 | Freemium-Grenze bestätigen | Abschnitt 6 | Assessment + Modul 1 frei; Module 2–7, Prüfung, Zertifikat Premium |
| E2 | Preis, Laufzeit, Zahlungsanbieter des Abos | Abschnitt 6 | — (Marktvergleich empfohlen) |
| E2a | MVP mit oder ohne integrierte Bezahlstrecke | Abschnitt 6, R6 | Ohne: manuelle Freischaltung im MVP, Bezahlintegration direkt danach |
| E3 | Rechtstexte: Impressum, Datenschutzerklärung, AGB (Verantwortlicher Rechtsträger, juristische Prüfung) | FR-1.4; L1/L4 | Juristisch erstellen lassen; nicht durch KI generieren |
| E4 | Prompt-Werkstatt ohne Live-LLM im MVP bestätigen | FR-9.4 | Ohne Live-LLM starten (Datenschutz/Kosten offen), als Ausbaustufe evaluieren |
| E5 | Redaktions-Workflow im MVP Git-basiert (ohne eigene Redaktions-UI) | FR-14.5, NFR-E2 | Git-basiert starten; Redaktions-UI als Ausbaustufe |
| E6 | Bestehensgrenze und Wiederholungsregeln der Abschlussprüfung | FR-11.3/11.4 | 80 %, Wiederholung nach 24 h, unbegrenzte Versuche |
| E7 | Zertifikats-Verifizierung per öffentlichem Link im MVP | FR-12.3 | Ja, einfache Verifikationsseite (geringer Aufwand, hoher Vertrauensgewinn) |
| E8 | Benennung Fachreviewer und Regulatorik-Reviewer | R4; open-questions R1/R2 | Vor Produktionsstart Phase 3 |
| E9 | Startzeitpunkt/Umfang der rollenbezogenen Filter-UI im MVP (volle Filter-UI vs. nur Rollen-Tags + einfacher Filter) | FR-2.3/2.4 | Einfacher Rollenfilter im MVP; volle Facetten-Suche später |

Diese Punkte sind zusätzlich in `docs/open-questions.md` verzeichnet
(P6–P8 und Folgeeinträge).
