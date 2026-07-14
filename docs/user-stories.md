# User Stories — MVP der VersicherungsTech KI-Akademie

**Status:** Entwurf zur Freigabe durch den Auftraggeber
**Stand:** 2026-07-14
**Grundlagen:** `docs/product-requirements.md` (FR-Nummern),
`docs/acceptance-criteria.md` (AC-Nummern)

Format: „Als *Rolle* möchte ich *Ziel*, damit *Nutzen*.“
Priorität: **M** = Must-have (MVP), **S** = Should-have (MVP, reduzierbar),
**C** = Could-have (nur bei Restkapazität; sonst Ausbaustufe).
Punkte mit Entscheidungsbedarf: **`ENTSCHEIDUNG AUFTRAGGEBER`**.

---

## Epic 1 — Landingpage und Katalog (FR-1, FR-2)

| ID | Story | Prio | Ref |
|---|---|---|---|
| US-1.1 | Als Gast möchte ich auf der Landingpage in unter einer Minute verstehen, was die Akademie ist, für wen sie ist und was sie kostet, damit ich entscheiden kann, ob sie für mich relevant ist. | M | AC-1 |
| US-1.2 | Als Gast möchte ich den Kurskatalog mit Kursdetails (Module, Lernzeit, Niveau, Free/Premium) einsehen, damit ich vor der Registrierung weiß, was mich erwartet. | M | AC-2 |
| US-1.3 | Als Gast möchte ich Impressum und Datenschutzerklärung erreichen, damit ich weiß, wer die Plattform betreibt und was mit meinen Daten geschieht. | M | AC-1 |
| US-1.4 | Als Gast möchte ich Inhalte nach meiner Rolle filtern, damit ich sofort sehe, was zu meinem Arbeitsalltag passt. | S | AC-2 |
| US-1.5 | Als Interessent aus dem VersicherungsTech Magazin möchte ich den Zusammenhang zwischen Magazin und Akademie erkennen, damit ich der Plattform vertraue. | S | AC-1 |

## Epic 2 — Konto und Abo (FR-16)

| ID | Story | Prio | Ref |
|---|---|---|---|
| US-2.1 | Als Gast möchte ich mich mit E-Mail und Passwort registrieren, damit ich Lernfortschritt speichern und freie Module vollständig nutzen kann. | M | AC-3 |
| US-2.2 | Als Lernende möchte ich mein Passwort zurücksetzen können, damit ich bei Verlust nicht ausgesperrt bin. | M | AC-3 |
| US-2.3 | Als Lernende möchte ich meine Rolle und meinen Organisationstyp freiwillig angeben, damit Lernpfad und Filter zu mir passen — ohne dass ich es muss. | M | AC-3 |
| US-2.4 | Als Free-Nutzer möchte ich transparent sehen, was Premium enthält und kostet, damit ich eine informierte Abo-Entscheidung treffe. | M | AC-4 — Preis: ENTSCHEIDUNG AUFTRAGGEBER (E2) |
| US-2.5 | Als Free-Nutzer möchte ich Premium abschließen können, damit ich den vollständigen Kurs nutzen kann. | M | AC-4 — Bezahlstrecke vs. manuelle Freischaltung: ENTSCHEIDUNG AUFTRAGGEBER (E2a) |
| US-2.6 | Als Premium-Nutzer möchte ich mein Abo einsehen und kündigen können, damit ich die Kontrolle über meine Kosten behalte. | M | AC-4 |
| US-2.7 | Als Nutzerin möchte ich mein Konto selbst löschen können, damit meine personenbezogenen Daten entfernt werden. | M | AC-3 |

## Epic 3 — Einstufung und Lernpfad (FR-3, FR-4)

| ID | Story | Prio | Ref |
|---|---|---|---|
| US-3.1 | Als neue Lernende möchte ich ein kurzes Einstufungsassessment machen, damit ich eine zu meinem Vorwissen passende Lernempfehlung bekomme. | M | AC-5 |
| US-3.2 | Als Lernende möchte ich mein Assessment-Ergebnis mit Begründung sehen, damit ich die Empfehlung nachvollziehen kann und mich nicht bewertet fühle. | M | AC-5 |
| US-3.3 | Als Lernende möchte ich einen persönlichen Lernpfad mit klarem nächsten Schritt sehen, damit ich nie überlegen muss, wo ich weitermache. | M | AC-6 |
| US-3.4 | Als Lernende ohne Lust auf Assessments möchte ich den Kurs auch direkt in Standardreihenfolge starten können, damit mich nichts aufhält. | M | AC-5 |
| US-3.5 | Als erfahrener KI-Nutzer möchte ich, dass mir Grundlagenmodule als optionale Auffrischung markiert werden, damit ich meine Zeit auf Neues verwende. | S | AC-6 |
| US-3.6 | Als Lernende mit angegebener Rolle möchte ich rollenspezifische Beispiele bevorzugt sehen, damit die Inhalte zu meinem Alltag passen. | S | AC-6 |

## Epic 4 — Lernen: Lektionen und Quizze (FR-5, FR-6)

| ID | Story | Prio | Ref |
|---|---|---|---|
| US-4.1 | Als Lernende möchte ich Lektionen in einheitlicher Struktur mit Lesezeit-Angabe lesen, damit ich Einheiten verlässlich in meine Arbeitspausen einplanen kann. | M | AC-7 |
| US-4.2 | Als Lernende möchte ich annotierte Beispiele (z. B. kommentierte Prompts und KI-Outputs) sehen, damit ich am konkreten Fall verstehe, was gut und was riskant ist. | M | AC-7 |
| US-4.3 | Als Lernende möchte ich in Lektionen kurze Quizfragen mit erklärendem Feedback beantworten, damit ich mein Verständnis sofort prüfe. | M | AC-8 |
| US-4.4 | Als Lernende möchte ich am Modulende einen Modul-Check machen, damit ich weiß, ob ich das Modul verstanden habe, bevor ich weitergehe. | M | AC-8 |
| US-4.5 | Als Lernende möchte ich jede Lektion über eine stabile URL erreichen und teilen können, damit ich Inhalte als Nachschlagewerk nutzen kann. | M | AC-7 |
| US-4.6 | Als Lernende möchte ich jede Einheit mit einer Transferaufgabe für meinen eigenen Arbeitskontext abschließen, damit das Gelernte im Alltag ankommt. | M | AC-7 |

## Epic 5 — Interaktive Übungen (FR-7, FR-8, FR-9)

| ID | Story | Prio | Ref |
|---|---|---|---|
| US-5.1 | Als Lernende möchte ich in verzweigten Fallsimulationen Entscheidungen treffen und deren Konsequenzen erleben, damit ich sicheres Verhalten gefahrlos üben kann. | M | AC-9 |
| US-5.2 | Als Lernende möchte ich nach einer Simulation eine Auswertung meiner Entscheidungen mit Erklärungen sehen, damit ich aus Fehlern lerne statt nur „falsch“ zu lesen. | M | AC-9 |
| US-5.3 | Als Lernende möchte ich Simulationen wiederholen und andere Pfade erkunden, damit ich alle Facetten des Falls verstehe. | S | AC-9 |
| US-5.4 | Als Lernende möchte ich in Datenampel-Übungen einordnen, welche Daten ich in KI-Tools eingeben darf, damit ich im Alltag schnell und sicher entscheide. | M | AC-10 |
| US-5.5 | Als Lernende möchte ich zu jeder Ampel-Einordnung die Begründung und eine sichere Alternative erfahren, damit ich das Muster auf neue Situationen übertragen kann. | M | AC-10 |
| US-5.6 | Als Lernende möchte ich kommentierte Prompt-Vorlagen für typische Versicherungsaufgaben finden und kopieren, damit ich sofort besser mit meinem freigegebenen KI-Tool arbeite. | M | AC-11 |
| US-5.7 | Als Lernende möchte ich in der Prompt-Werkstatt einen Prompt aus Bausteinen zusammensetzen und strukturbezogenes Feedback bekommen, damit ich gutes Prompten aktiv übe. | M | AC-11 — MVP ohne Live-LLM: ENTSCHEIDUNG AUFTRAGGEBER (E4) |
| US-5.8 | Als Lernende möchte ich bei jeder Übung den Hinweis auf synthetische Daten und interne Unternehmensrichtlinien sehen, damit ich Lernmodell und verbindliche Regeln nicht verwechsle. | M | AC-10 |

## Epic 6 — Fortschritt, Prüfung, Nachweis (FR-10, FR-11, FR-12)

| ID | Story | Prio | Ref |
|---|---|---|---|
| US-6.1 | Als Lernende möchte ich meinen Fortschritt je Modul und für den Kurs sehen, damit ich weiß, wo ich stehe und was noch fehlt. | M | AC-12 |
| US-6.2 | Als Lernende möchte ich mit einem Klick bei meiner nächsten offenen Einheit weitermachen, damit der Wiedereinstieg keine Hürde ist. | M | AC-12 |
| US-6.3 | Als Lernende möchte ich meinen Fortschritt auf jedem Gerät wiederfinden, damit ich zwischen Büro-PC und Smartphone wechseln kann. | M | AC-12 |
| US-6.4 | Als Premium-Lernende möchte ich nach Abschluss aller Module eine Abschlussprüfung ablegen, damit mein Gesamtverständnis geprüft wird. | M | AC-13 — Bestehensgrenze: ENTSCHEIDUNG AUFTRAGGEBER (E6) |
| US-6.5 | Als Lernende möchte ich bei Nichtbestehen eine Auswertung nach Themenfeldern und eine Wiederholungsmöglichkeit, damit die Prüfung mich weiterbringt statt abzuschrecken. | M | AC-13 |
| US-6.6 | Als Lernende möchte ich je abgeschlossenem Modul ein Badge erhalten, damit ich Zwischenerfolge sehe. | S | AC-14 |
| US-6.7 | Als Lernende möchte ich nach bestandener Prüfung ein PDF-Zertifikat mit Kursversion und Datum herunterladen, damit ich die Weiterbildung belegen kann. | M | AC-14 — Nachweisform: ENTSCHEIDUNG AUFTRAGGEBER (P7/E7) |
| US-6.8 | Als Arbeitgeberin einer Absolventin möchte ich die Echtheit eines Zertifikats über einen Link prüfen können, damit ich dem Nachweis vertrauen kann. | C | AC-14 — ENTSCHEIDUNG AUFTRAGGEBER (E7) |

## Epic 7 — Vertrauen: Quellen, Version, Review (FR-13, FR-14)

| ID | Story | Prio | Ref |
|---|---|---|---|
| US-7.1 | Als Lernende möchte ich an jeder Lektion Version, Änderungsdatum und (bei Rechtsthemen) den Rechtsstand sehen, damit ich die Aktualität einschätzen kann. | M | AC-15 |
| US-7.2 | Als Lernende möchte ich die Quellen einer Lektion mit Fundstellen einsehen, damit ich Aussagen nachprüfen kann. | M | AC-15 |
| US-7.3 | Als Autorin möchte ich Inhalte im Entwurfsstatus anlegen und zur Prüfung einreichen, damit nichts Ungeprüftes live geht. | M | AC-16 |
| US-7.4 | Als Reviewerin möchte ich Inhalte freigeben oder mit Kommentar zurückweisen, damit der Review-Prozess dokumentiert und wirksam ist. | M | AC-16 |
| US-7.5 | Als Regulatorik-Reviewer möchte ich, dass Inhalte mit Regulatorik-Marker ohne meine Freigabe technisch nicht veröffentlicht werden können, damit die Sicherheitsregeln durchgesetzt sind. | M | AC-16 |
| US-7.6 | Als Redaktion möchte ich, dass Inhalte mit `QUELLE ZU VERIFIZIEREN` die Veröffentlichung blockieren, damit keine unbelegten Aussagen live gehen. | M | AC-16 |

## Epic 8 — Suche (FR-15)

| ID | Story | Prio | Ref |
|---|---|---|---|
| US-8.1 | Als Nutzerin möchte ich per Volltextsuche Lektionen, Vorlagen und Checklisten finden, damit die Plattform auch als Nachschlagewerk funktioniert. | M | AC-17 |
| US-8.2 | Als Nutzerin möchte ich Suchergebnisse nach Rolle und Inhaltstyp filtern, damit ich schneller das Passende finde. | S | AC-17 |
| US-8.3 | Als Free-Nutzerin möchte ich Premium-Treffer mit Kennzeichnung sehen, damit ich weiß, was mir ein Abo zusätzlich erschließen würde. | S | AC-17 |

## Epic 9 — Barrierefreiheit und mobile Nutzung (NFR-A, NFR-B)

Querschnittsthema — gilt als Anforderung an jede Story oben; eigene Stories
für die Prüfbarkeit:

| ID | Story | Prio | Ref |
|---|---|---|---|
| US-9.1 | Als Screenreader-Nutzer möchte ich alle Lerninhalte und Übungen vollständig nutzen können, damit ich gleichberechtigt lernen kann. | M | AC-18 |
| US-9.2 | Als Nutzerin, die nur die Tastatur verwendet, möchte ich Quiz, Simulation, Datenampel und Prompt-Werkstatt vollständig bedienen können, damit keine Übung für mich gesperrt ist. | M | AC-18 |
| US-9.3 | Als Pendlerin möchte ich alle Kernflows auf dem Smartphone nutzen, damit ich unterwegs lernen kann. | M | AC-19 |
| US-9.4 | Als Nutzer mit Farbsehschwäche möchte ich die Datenampel auch ohne Farbwahrnehmung sicher bedienen, damit die zentrale Übung des Kurses für mich funktioniert. | M | AC-18 |

## Epic 10 — Datenschutz (NFR-D)

| ID | Story | Prio | Ref |
|---|---|---|---|
| US-10.1 | Als Nutzerin möchte ich, dass nur die für das Lernen nötigen Daten über mich gespeichert werden, damit meine Weiterbildung nicht zur Überwachung wird. | M | AC-20 |
| US-10.2 | Als Nutzerin möchte ich sicher sein, dass mein Arbeitgeber meinen Lernstand nicht einsehen kann, damit ich angstfrei üben und Fehler machen kann. | M | AC-20 |
| US-10.3 | Als Nutzerin möchte ich Auskunft über meine gespeicherten Daten erhalten können, damit ich meine Rechte wahrnehmen kann. | M | AC-20 |
