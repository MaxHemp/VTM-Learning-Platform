# CLAUDE.md — VersicherungsTech KI-Akademie

Diese Datei ist die verbindliche Arbeitsgrundlage für Claude Code (und andere
KI-Assistenten) in diesem Repository. Sie gilt für alle Aufgaben: Code,
Inhalte, Dokumentation und Redaktion.

## 1. Projektüberblick

**Projektname:** VersicherungsTech KI-Akademie
**Herausgeber:** VersicherungsTech Magazin — https://www.versicherungstech-magazin.de
**Ziel:** Eine KI-Learning-Plattform für die DACH-Versicherungsbranche, die
Fachkräften praxisnah vermittelt, wie sie KI in ihrem Arbeitsalltag sicher,
sinnvoll und regelkonform einsetzen.

**Zielgruppe:** Versicherer, Agenturen, Makler, Assekuradeure, InsurTechs und
versicherungsnahe Dienstleister im DACH-Raum. Details: `docs/target-groups.md`

**Aktueller Projektstand:** Konzeptions- und Dokumentationsphase.
Es existiert noch keine Anwendung und es werden noch keine vollständigen
Kurse geschrieben. Erst Grundlagen und Regeln, dann Architektur, dann Inhalte.

## 2. Zentrale Formatvorgabe: Kein Video

Die gesamte Plattform funktioniert **ohne Video**. Das ist eine bewusste
Produktentscheidung, keine vorläufige Einschränkung.

- Keine Videos, keine Video-Platzhalter, keine „später ergänzen wir ein
  Video“-Konzepte.
- Keine Formate, die Video voraussetzen (z. B. Screencast-Analysen,
  Video-Rollenspiele, Webinar-Aufzeichnungen).

**Zulässige Lernformate:**

- schriftliche Lektionen
- annotierte Beispiele
- Fallstudien
- Prompt-Vorlagen
- Checklisten
- Quizze
- Entscheidungsbäume
- verzweigte Fallsimulationen
- praktische Aufgaben mit freigegebenen KI-Tools
- interaktive Dokumentenübungen
- Prozesskarten
- schriftliche Rollenspiele
- Transferaufgaben

Didaktische Leitlinien: `docs/didactic-principles.md`

## 3. Tonalität und Redaktion

Alle Inhalte sind:

- kompakt
- verständlich
- praxisnah
- fachlich
- umsetzungsorientiert
- Hands-on

Nicht erlaubt: Marketingfloskeln, unnötiger Technikjargon, Buzzword-Prosa,
leere Superlative. Fachbegriffe der Versicherungsbranche sind erwünscht,
werden aber bei Erstverwendung kurz erklärt, wenn sie nicht rollenübergreifend
geläufig sind.

Redaktionelle Details: `docs/editorial-guidelines.md`

## 4. Sicherheits- und Datenschutzregeln (verbindlich)

Vollständige Fassung: `docs/security-and-privacy-rules.md` — Kurzfassung:

### Übungsdaten
- Ausschließlich **synthetische Übungsdaten** verwenden.
- Keine realistisch wirkenden vollständigen Identitäten erzeugen
  (keine Kombination aus echt wirkendem Namen + Adresse + Geburtsdatum +
  Vertrags-/Schadendaten).
- Keine realen Kunden-, Gesundheits-, Schaden- oder Vertragsdaten verwenden.
- Synthetische Daten als solche kennzeichnen.

### Secrets
- Keine Zugangsdaten, API-Keys, Tokens oder andere Secrets im Repository.
- Geheimnisse ausschließlich über Umgebungsvariablen.
- `.env`-Dateien gehören in `.gitignore`; Vorlagen als `.env.example` ohne Werte.

### Regulatorik und Recht
- Keine rechtlich verbindlichen Aussagen ohne Quellenangabe und Rechtsstand
  (Datum).
- Inhalte mit regulatorischen Aussagen tragen die Kennzeichnung
  **`REVIEW ERFORDERLICH: Regulatorik`** und gelten bis zur fachlichen
  Freigabe als Entwurf.
- Für regulatorische Aussagen möglichst **Primärquellen** verwenden
  (EUR-Lex, Gesetzestexte, Aufsichtsbehörden wie BaFin/FMA/FINMA, EDSA/DSK).
- Keine Quellen, Fundstellen, Gerichtsurteile oder Behördenaussagen erfinden.
- Nicht verifizierbare Quellen kennzeichnen mit: **`QUELLE ZU VERIFIZIEREN`**.
- Niemals behaupten, ein Kurs, ein Prozess oder ein System sei automatisch
  „AI-Act-konform“ oder „DSGVO-konform“. Zulässig sind Formulierungen wie
  „unterstützt bei der Umsetzung von Anforderungen aus …“.

### Menschliche Kontrolle (Human in the Loop)
- KI wird **niemals** als alleinige Instanz dargestellt für: Deckung,
  Leistung, Pricing, Underwriting, Betrugsverdacht oder Kundenberatung.
- Jede kundenrelevante oder entscheidungsnahe KI-Anwendung in Lerninhalten
  und Beispielen definiert einen expliziten **menschlichen Kontroll- oder
  Freigabepunkt** (wer prüft, was, wann, mit welcher Eingriffsmöglichkeit).

## 5. Technische Arbeitsregeln

- **Repository-Zustand zuerst prüfen.** Vor jeder Aufgabe den bestehenden
  Stand sichten (Struktur, Konventionen, offene Branches).
- **Keine Architekturänderungen ohne Begründung.** Bestehende Architektur
  respektieren; Abweichungen begründen und als ADR dokumentieren.
- **Keine destruktiven Befehle ohne ausdrückliche Bestätigung**
  (z. B. `rm -rf`, `git push --force`, Löschen von Branches, Daten-Resets).
- **Kein Deployment ohne ausdrückliche Freigabe.**
- **Trennung der Schichten:** Inhalte (Content), Präsentation (UI) und
  Anwendungslogik bleiben getrennt. Inhalte werden strukturiert und
  versionierbar abgelegt (z. B. Markdown/strukturierte Daten), nicht in
  Komponenten hartkodiert.
- **Wartbarer, getesteter, dokumentierter Code:** Neue Logik kommt mit Tests;
  öffentliche Schnittstellen und nicht offensichtliche Entscheidungen werden
  dokumentiert.
- **Barrierefreiheit:** Inhalte und UI werden für Screenreader, Tastatur-
  bedienung und ausreichende Kontraste konzipiert (Orientierung: WCAG 2.1 AA).
  Das textbasierte Format ist hier ein Vorteil — nicht verspielen.
- **Datenschutz by Design:** Datensparsamkeit, keine unnötige Erfassung von
  Lernendendaten, Rechtsgrundlagen und Löschkonzepte mitdenken.
- **Mobile Nutzung:** Inhalte und UI müssen auf Smartphones gut lesbar und
  bedienbar sein.
- **ADRs:** Wesentliche Architekturentscheidungen als Architecture Decision
  Records unter `docs/adr/` festhalten (Nummerierung `NNNN-titel.md`).
- **Kleine, überprüfbare Schritte:** Kleine Commits mit klaren Messages;
  große Aufgaben in nachvollziehbare Etappen zerlegen.

## 6. Repository-Struktur (Zielbild)

```
/
├── CLAUDE.md                        # Diese Datei — verbindliche Arbeitsregeln
├── README.md                        # Projekteinstieg
├── docs/
│   ├── project-vision.md            # Vision, Ziele, Nicht-Ziele
│   ├── target-groups.md             # Zielgruppen und Rollenprofile
│   ├── editorial-guidelines.md      # Redaktionsleitfaden
│   ├── didactic-principles.md       # Didaktische Prinzipien und Formate
│   ├── security-and-privacy-rules.md# Sicherheits- und Datenschutzregeln
│   ├── definition-of-done.md        # DoD für Code und Inhalte
│   ├── open-questions.md            # Offene Fragen und Entscheidungen
│   └── adr/                         # Architecture Decision Records (später)
├── content/                         # Lerninhalte (später, strukturiert)
└── app/ bzw. src/                   # Anwendung (später, Architektur offen)
```

`content/` und `app//src/` existieren noch nicht — sie werden erst nach den
entsprechenden Architektur- und Curriculum-Entscheidungen angelegt.

## 7. Definition of Done (Kurzfassung)

Vollständig: `docs/definition-of-done.md`

**Inhalte:** fachlich korrekt, Zielgruppe/Rolle benannt, Format zulässig
(kein Video), Tonalität eingehalten, nur synthetische Daten, regulatorische
Aussagen mit Quelle + Rechtsstand + Review-Kennzeichnung, menschlicher
Kontrollpunkt bei entscheidungsnahen KI-Beispielen, Transferaufgabe bzw.
Praxisbezug vorhanden.

**Code:** getestet, dokumentiert, barrierefrei, mobil nutzbar, keine Secrets,
Schichtentrennung eingehalten, ADR bei Architekturentscheidungen.

## 8. Arbeitsmodus für Claude in diesem Repository

1. Vor Änderungen: bestehende Dokumente in `docs/` lesen, die die Aufgabe
   betreffen.
2. Bei Widersprüchen zwischen Aufgabenstellung und dieser Datei: nachfragen,
   nicht stillschweigend entscheiden.
3. Unsicherheiten, Annahmen und offene Punkte in `docs/open-questions.md`
   ergänzen statt sie zu verschweigen.
4. Keine vollständigen Kurse und keine Anwendung implementieren, solange
   die Konzeptionsphase nicht ausdrücklich abgeschlossen wurde.
5. Deutsch ist die Arbeits- und Inhaltssprache. Code, Bezeichner und
   Commit-Messages auf Englisch; Dokumentation und Inhalte auf Deutsch.
