# Didaktische Prinzipien — VersicherungsTech KI-Akademie

**Status:** Entwurf · Konzeptionsphase
**Stand:** 2026-07-14

## 1. Leitidee

Die Akademie vermittelt KI-Kompetenz **vom Arbeitsalltag aus**: Ausgangspunkt
jeder Lerneinheit ist eine reale Aufgabe der jeweiligen Rolle (z. B. „eine
Schadenmeldung strukturiert erfassen“), nicht eine Technologie. Gelernt wird
durch Lesen, Anwenden, Entscheiden und Übertragen — vollständig ohne Video.

## 2. Grundprinzipien

1. **Rollenbezug vor Technikbezug.** Lernpfade sind nach Rollen organisiert
   (siehe `docs/target-groups.md`), nicht nach KI-Themen. KI-Grundlagen
   werden dort vermittelt, wo die Rolle sie braucht.
2. **Anwendung vor Theorie.** Jede Einheit enthält mindestens ein
   anwendbares Element; Theorie wird auf das reduziert, was für sicheres
   Handeln nötig ist.
3. **Kleine Einheiten.** Eine Lerneinheit ist in ca. 10–20 Minuten
   absolvierbar (`ANNAHME`, zu validieren). Längere Themen werden in
   Serien zerlegt.
4. **Aktives Lernen.** Lesen wird konsequent mit Interaktion verschränkt:
   Quizfragen, Entscheidungen, Übungen — nicht als Anhang, sondern im
   Lernfluss.
5. **Verantwortung ist Lernstoff.** Grenzen der KI, Kontrollpunkte,
   Datenschutz und Regulatorik sind in jede Einheit integriert, nicht in
   ein separates „Compliance-Modul“ ausgelagert (ein solches Modul kann es
   zusätzlich geben).
6. **Transfer ist Pflicht.** Jede Einheit endet mit einer Transferaufgabe
   für den eigenen Arbeitskontext.
7. **Fehlerfreundlichkeit.** Übungen und Simulationen sind sichere Räume:
   Falsche Entscheidungen führen zu erklärendem Feedback, nicht nur zu
   „falsch“.
8. **Textstärke nutzen.** Text ist durchsuchbar, zitierbar, überfliegbar,
   barrierearm und schnell aktualisierbar. Inhalte werden so geschrieben,
   dass diese Stärken wirken (klare Struktur, Anker, Zusammenfassungen,
   Nachschlagbarkeit).

## 3. Formatbaukasten (alle ohne Video)

| Format | Einsatz | Hinweise |
|---|---|---|
| Schriftliche Lektion | Grundbaustein jeder Einheit | Struktur laut Redaktionsleitfaden |
| Annotiertes Beispiel | Prompts, Dokumente, KI-Outputs mit Randkommentaren | Zeigt das „Warum“ hinter gutem/schlechtem Vorgehen |
| Fallstudie | Realistische (synthetische) Branchenszenarien | Immer mit `SYNTHETISCHE DATEN` gekennzeichnet |
| Prompt-Vorlage | Direkt nutzbare, kommentierte Prompts je Aufgabe | Mit Hinweisen zu Grenzen und Prüfschritten |
| Checkliste | Prüf- und Arbeitsschritte für den Alltag | Druck-/exportfähig denken |
| Quiz | Wissensprüfung mit erklärendem Feedback | Feedback erklärt auch richtige Antworten |
| Entscheidungsbaum | „Darf/soll ich KI hier einsetzen?“-Logiken | Auch als Prozesskarte darstellbar |
| Verzweigte Fallsimulation | Entscheidungen mit Konsequenzen im Szenario | Kernformat für entscheidungsnahe Rollen |
| Praktische Aufgabe mit freigegebenen KI-Tools | Angeleitetes Arbeiten im echten Tool | Nur mit synthetischen Daten; Tool-Freigabeliste nötig |
| Interaktive Dokumentenübung | Arbeit an synthetischen Anträgen, Bedingungen, Schadenmeldungen | z. B. „Finde die 3 Prüfpunkte in diesem KI-Output“ |
| Prozesskarte | Visualisierte Abläufe mit KI- und Kontrollpunkten | Kontrollpunkte farblich/symbolisch hervorheben |
| Schriftliches Rollenspiel | Dialogsimulation in Textform (z. B. Kundengespräch) | Auch als verzweigtes Format möglich |
| Transferaufgabe | Anwendung im eigenen Arbeitskontext | Pflichtabschluss jeder Einheit |

**Nicht zulässig:** Videos, Video-Platzhalter, Audio-only-Formate als
Pflichtbestandteil, sowie Konzepte, die Video voraussetzen.

## 4. Aufbau eines Lernpfads (Arbeitsmodell)

```
Lernpfad (je Rolle, z. B. „KI im Schadenmanagement“)
├── Niveau 1: Grundlagen   — Was kann KI hier, was nicht? Sicherer Umgang.
├── Niveau 2: Anwendung    — Konkrete Aufgaben mit Vorlagen und Übungen.
└── Niveau 3: Vertiefung   — Komplexe Fälle, Grenzfälle, Governance.

Jede Einheit:
Nutzenversprechen → Kerninhalt → Praxisteil → Grenzen & Kontrolle
→ Zusammenfassung → Transferaufgabe
```

Zusätzlich rollenübergreifende Basismodule (`ANNAHME`, Zuschnitt offen):

- KI-Grundlagen für die Versicherungsbranche
- Prompting-Grundlagen
- Datenschutz und KI im Arbeitsalltag
- Regulatorischer Rahmen (EU AI Act, DSGVO — `REVIEW ERFORDERLICH: Regulatorik`)

## 5. Lernstandserhebung und Feedback

- **Formativ statt punitiv:** Quizze und Simulationen dienen dem Lernen;
  Ergebnisse erzeugen erklärendes Feedback.
- **Feedbacktiefe:** Jede Quiz-/Simulationsantwort erhält eine Begründung —
  auch richtige Antworten („richtig, weil …“).
- **Abschlussnachweise:** Ob und in welcher Form es Zertifikate/Nachweise
  gibt, ist offen (siehe `docs/open-questions.md`).
- **Datensparsamkeit:** Lernstandsdaten werden nur erhoben, soweit sie dem
  Lernen dienen (siehe `docs/security-and-privacy-rules.md`).

## 6. Barrierefreiheit als didaktisches Prinzip

- Klare Sprache und konsistente Struktur helfen allen Lernenden.
- Alle interaktiven Formate (Quiz, Simulationen, Entscheidungsbäume) müssen
  per Tastatur und Screenreader nutzbar sein.
- Prozesskarten und andere visuelle Elemente erhalten gleichwertige
  Textalternativen.
- Kein Inhalt darf ausschließlich über Farbe, Bild oder Interaktion
  verständlich sein.

## 7. Qualitätsmaßstab je Einheit

Eine Lerneinheit ist didaktisch fertig, wenn (Details:
`docs/definition-of-done.md`):

- das Nutzenversprechen konkret und rollenbezogen ist,
- mindestens ein anwendbares Praxiselement enthalten ist,
- Grenzen der KI und der menschliche Kontrollpunkt benannt sind,
- eine Transferaufgabe existiert,
- alle Interaktionen erklärendes Feedback geben,
- die Einheit im Zeitrahmen absolvierbar ist.
