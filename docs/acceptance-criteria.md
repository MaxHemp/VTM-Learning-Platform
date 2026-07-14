# Akzeptanzkriterien — MVP der VersicherungsTech KI-Akademie

**Status:** Entwurf zur Freigabe durch den Auftraggeber
**Stand:** 2026-07-14
**Grundlagen:** `docs/product-requirements.md` (FR/NFR),
`docs/user-stories.md` (US), `docs/definition-of-done.md`

Diese Kriterien sind die Abnahmegrundlage je Funktionsbereich. Sie ergänzen
die Definition of Done — beide müssen erfüllt sein. Kriterien sind als
prüfbare Aussagen formuliert („Gegeben … wenn … dann …“ wo sinnvoll).

---

## AC-1 Landingpage (FR-1)

1. Ein Gast erreicht die Landingpage ohne Login; sie nennt Zielgruppe
   (DACH-Versicherungsbranche), Nutzen und Freemium-Modell in den ersten
   sichtbaren Abschnitten.
2. Von der Landingpage sind Kurskatalog und Registrierung mit je einem
   Klick/Tap erreichbar.
3. Impressum und Datenschutzerklärung sind von jeder Seite aus verlinkt
   und erreichbar.
4. Die Seite enthält keine Videos, keine Video-Platzhalter, keine
   Marketingfloskeln und keine Konformitätsversprechen
   („DSGVO-konform lernen“ o. ä.).
5. Der Bezug zum VersicherungsTech Magazin ist erkennbar (Herausgeber-Angabe).

## AC-2 Kurskatalog und Filter (FR-2)

1. Der Katalog zeigt jeden veröffentlichten Kurs mit Titel,
   Kurzbeschreibung, Modulanzahl, geschätzter Gesamtlernzeit, Niveau und
   Free/Premium-Kennzeichnung.
2. Die Kursdetailseite listet alle Module mit Lernzielen und
   Free/Premium-Status je Modul.
3. Gegeben ein Gast wählt den Rollenfilter „Schadenmanagement“, dann werden
   nur Inhalte mit diesem Rollen-Tag (oder rollenübergreifende Inhalte,
   als solche gekennzeichnet) angezeigt.
4. Nicht veröffentlichte Inhalte (Status ≠ `Veröffentlicht`) erscheinen
   unter keinen Umständen im Katalog, in Detailseiten oder in der Suche.

## AC-3 Konto (FR-16)

1. Registrierung erfordert E-Mail-Verifizierung; ohne Verifizierung kein
   Zugriff auf gespeicherten Lernfortschritt.
2. Passwort-Reset per E-Mail funktioniert; Passwörter werden nie im
   Klartext gespeichert oder geloggt.
3. Rolle und Organisationstyp sind bei Registrierung und im Profil
   **optional**; das Weglassen blockiert keinen Flow.
4. Kontolöschung ist in Selbstbedienung möglich; nach Löschung sind
   personenbezogene Daten gemäß Löschkonzept entfernt und ein Login ist
   nicht mehr möglich.
5. Es werden keine werblichen E-Mails ohne separates Double-Opt-in
   versendet.

## AC-4 Freemium und Abo (FR-16.4, Abschnitt 6 PRD)

1. Gegeben ein Free-Konto, wenn es Modul 1 und das Assessment nutzt, dann
   ist beides vollständig und ohne Zahlungsaufforderung mitten in einer
   Einheit nutzbar.
2. Gegeben ein Free-Konto öffnet eine Premium-Einheit, dann erscheint eine
   klare Premium-Seite mit Leistungen, Preis und Kündigungsbedingungen —
   keine irreführenden Muster (kein Countdown-Druck, keine versteckten
   Kosten).
3. Nach Premium-Abschluss (bzw. manueller Freischaltung — E2a) ist der
   zuvor gesperrte Inhalt ohne erneuten Login sofort nutzbar.
4. Kündigung ist auf demselben Weg möglich wie der Abschluss (kein
   „Kündigungslabyrinth“); nach Ablauf fällt das Konto auf Free zurück,
   Lernfortschritt bleibt erhalten.

## AC-5 Einstufungsassessment (FR-3)

1. Das Assessment umfasst 10–15 Fragen und ist in ≤ 10 Minuten abschließbar.
2. Das Ergebnis nennt Einstufung und Begründung in wertschätzender Sprache;
   es enthält keine Formulierung, die als Leistungsbewertung lesbar ist
   (Review durch Redaktion).
3. Das Assessment ist wiederholbar; der Lernpfad aktualisiert sich nach
   Wiederholung auf Basis des neuen Ergebnisses.
4. Gegeben eine Nutzerin überspringt das Assessment, dann erhält sie den
   Standard-Lernpfad und kann das Assessment später jederzeit nachholen.
5. Assessment-Antworten werden nur zur Lernpfad-Erzeugung gespeichert und
   sind für niemanden außer der Nutzerin einsehbar.

## AC-6 Persönlicher Lernpfad (FR-4)

1. Nach Assessment oder Kursstart existiert ein Lernpfad, der die nächste
   empfohlene Einheit eindeutig benennt.
2. Gegeben die Einstufung „Fortgeschritten“, dann ist Modul 1 als optionale
   Auffrischung markiert, aber weiterhin zugänglich.
3. Gegeben eine Nutzerin mit Rolle „Makler und Vermittler“, wenn eine
   Lektion rollenspezifische Beispielvarianten hat, dann wird die
   Makler-Variante vorausgewählt (andere bleiben wählbar).
4. Freie Navigation ist möglich: Jede zugängliche Einheit ist auch außerhalb
   der Pfadreihenfolge startbar (Ausnahme: Abschlussprüfung, AC-13.1).
5. Premium-Einheiten sind im Pfad sichtbar und ehrlich gekennzeichnet; ein
   Klick führt Free-Nutzer zur Premium-Seite (AC-4.2), nicht zu einem Fehler.

## AC-7 Lektionen (FR-5)

1. Jede Lektion enthält die sechs Strukturelemente (Nutzenversprechen,
   Kerninhalt, Praxisteil, Grenzen & Kontrolle, Zusammenfassung,
   Transferaufgabe) — automatisiert prüfbar über das Content-Modell.
2. Lesezeit-Schätzung ist je Lektion sichtbar; Median der realen bearbeiteten
   Zeit liegt im Bereich 10–20 Minuten (Stichprobe im Pilot).
3. Jede Lektion hat eine stabile, teilbare URL; nicht berechtigte Aufrufe
   (Gast/Free auf Premium) landen auf einer erklärenden Seite, nie auf einem
   technischen Fehler.
4. Pflicht-Marker (`SYNTHETISCHE DATEN`, `RECHTSSTAND`, Quellen) werden aus
   den Metadaten gerendert und sind auf mobilen Viewports sichtbar.
5. Das Content-Modell akzeptiert keine Video-/Audio-Inhaltstypen; ein
   Einbettungsversuch schlägt im Content-Build mit klarer Fehlermeldung fehl.

## AC-8 Quizze (FR-6)

1. Alle vier Fragetypen (Single, Multiple, Richtig/Falsch, Zuordnung)
   funktionieren auf Desktop und Smartphone, mit Maus, Touch und Tastatur.
2. Jede Antwortoption liefert erklärendes Feedback — geprüft: Es existiert
   kein Quiz-Item ohne Feedbacktext für alle Optionen (Content-Build-Regel).
3. Lektions-Quizze sind unbegrenzt wiederholbar und speichern nur den Status
   „bearbeitet“; Modul-Checks speichern das Ergebnis für den Fortschritt.
4. Gegeben eine falsche Antwort im Modul-Check, dann verweist das Feedback
   auf die zugehörige Lektion („Zum Nachlesen: …“).

## AC-9 Verzweigte Fallsimulationen (FR-7)

1. Jede Simulation hat mindestens zwei echte Entscheidungsebenen und
   mindestens drei unterschiedliche Endauswertungen.
2. Jede Endauswertung fasst die getroffenen Entscheidungen zusammen,
   erklärt die Konsequenzen und beschreibt den sicheren Weg —
   fehlerfreundlich formuliert (redaktionell geprüft).
3. Gegeben der Pfad „KI-Ergebnis ungeprüft übernehmen“, dann zeigt die
   Simulation eine konkrete negative Konsequenz und benennt den fehlenden
   menschlichen Kontrollpunkt (Wer/Was/Wann/Wie).
4. „Andere Entscheidung ausprobieren“ ist nach Abschluss verfügbar und
   startet an einem wählbaren Entscheidungspunkt, nicht zwingend am Anfang.
5. Jede Simulation trägt sichtbar `SYNTHETISCHE DATEN`.
6. Simulationen sind vollständig deklarativ im Content-Modell definiert —
   eine neue Simulation erfordert keine Code-Änderung.

## AC-10 Datenampel-Übungen (FR-8)

1. Jede Übung enthält 8–12 Items; jedes Item ist Grün, Gelb oder Rot
   zuordenbar; bei Gelb muss die Bedingung aus angebotenen Optionen gewählt
   werden.
2. Jedes Item-Feedback nennt: korrekte Einstufung, Begründung
   (z. B. Personenbezug, besondere Kategorien) und sicheres
   Alternativvorgehen.
3. Der Hinweis „Lernmodell — verbindlich sind die Richtlinien Ihres
   Unternehmens“ ist in jeder Übung sichtbar, auch mobil.
4. Ampelwerte sind nie nur farblich codiert: Textlabel und Symbol/Muster
   sind immer vorhanden; die Übung ist mit Tastatur und Screenreader
   vollständig lösbar (Auswahlinteraktion, kein Drag-and-drop-Zwang).
5. Kein Item enthält realistisch wirkende vollständige Identitäten; alle
   Items sind synthetisch (Redaktions- und Sicherheitsreview).

## AC-11 Prompt-Werkstatt (FR-9)

1. Die Vorlagen-Bibliothek zeigt je Vorlage: Einsatzzweck, Grenzen,
   Prüfschritte und Rollen-Tags; Vorlagen sind über die Suche auffindbar.
2. Die Kopierfunktion übernimmt den Prompt vollständig in die
   Zwischenablage und zeigt dabei den stehenden Sicherheitshinweis
   (keine realen Kundendaten; Ergebnis fachlich prüfen).
3. Der Prompt-Bausatz erzwingt keine feste Reihenfolge, gibt aber
   regelbasiertes Feedback mindestens zu: fehlendem Kontext, fehlendem
   Prüfauftrag und Eingabedaten der Kategorie Rot (Querbezug Datenampel).
4. Die Werkstatt ruft nachweislich kein externes KI-Modell auf
   (keine entsprechenden Netzwerkaufrufe) — solange E4 nicht anders
   entschieden ist.
5. Alle Interaktionen sind tastatur- und screenreader-bedienbar.

## AC-12 Lernfortschritt (FR-10)

1. Der Status jeder Einheit (offen/begonnen/abgeschlossen) ist auf der
   Fortschrittsseite und im Lernpfad konsistent.
2. „Weiterlernen“ führt mit einem Klick zur nächsten offenen Einheit —
   auf Desktop und Smartphone.
3. Gegeben ein Login auf einem zweiten Gerät, dann ist der Fortschritt
   identisch (geräteübergreifende Speicherung am Konto).
4. Es werden keine Antwort-Detailprotokolle über das definierte Maß hinaus
   gespeichert (Prüfung gegen Datenmodell; Abgleich mit
   `docs/security-and-privacy-rules.md`).
5. Kein anderer Nutzer (und kein Arbeitgeber-Zugang — existiert nicht im
   MVP) kann individuelle Fortschritte einsehen.

## AC-13 Abschlussprüfung (FR-11)

1. Die Prüfung ist erst startbar, wenn alle sieben Module abgeschlossen sind;
   vorher zeigt die Prüfungsseite die fehlenden Module.
2. Die Prüfung kombiniert Fragenpool-Quiz und die Prüfungssimulation
   „Ein Vorgang, fünf Risiken“; zwei aufeinanderfolgende Versuche derselben
   Person enthalten nicht dieselbe Fragenauswahl in derselben Reihenfolge.
3. Bestehensgrenze und Wiederholungsregeln entsprechen der Entscheidung E6;
   sie werden vor Prüfungsbeginn angezeigt.
4. Gegeben ein nicht bestandener Versuch, dann zeigt die Auswertung die
   Themenfelder mit Schwächen und verlinkt die zugehörigen Lektionen;
   die Wiederholung ist nach der definierten Frist möglich.
5. Die Prüfung enthält keine Formulierung, die den Nachweis als amtliches
   Zertifikat oder IDD-Weiterbildung erscheinen lässt.
6. Ein Prüfungsabbruch (Verbindungsverlust) führt nicht zum Verlust des
   Versuchs: Wiederaufnahme oder Neustart ohne Zählung als Fehlversuch.

## AC-14 Badges und Zertifikat (FR-12)

1. Nach jedem bestandenen Modul-Check erscheint das Modul-Badge in der
   Fortschrittsübersicht.
2. Nach bestandener Abschlussprüfung ist das PDF-Zertifikat herunterladbar
   und enthält: Name, Kurstitel, Datum, Kursversion, Aussteller.
3. Der Zertifikatstext wurde vor Launch dem Regulatorik-Review unterzogen
   (keine Konformitäts-/Kompetenzgarantien).
4. Falls E7 = ja: Der Verifikationslink zeigt ohne Login Gültigkeit,
   Kurstitel und Ausstellungsdatum — aber keine weiteren personenbezogenen
   Daten als den Namen, und nur diesen, wenn die/der Lernende der
   Verifikationsseite zugestimmt hat.

## AC-15 Quellen- und Versionsangaben (FR-13)

1. Jede veröffentlichte Lektion zeigt Version und Datum der letzten
   inhaltlichen Änderung.
2. Jede Lektion mit regulatorischen Aussagen zeigt `RECHTSSTAND: JJJJ-MM-TT`
   und ein Quellenverzeichnis mit Fundstellen — automatisiert geprüft:
   Regulatorik-Marker ohne Rechtsstand oder ohne Quellen bricht den
   Content-Build ab.
3. Quellen sind strukturiert erfasst (Titel, Herausgeber, Fundstelle,
   Abrufdatum/Stand) und werden einheitlich gerendert.
4. Kein veröffentlichter Inhalt enthält den Marker `QUELLE ZU VERIFIZIEREN`
   (Build-Blocker, AC-16.4).

## AC-16 Review-Workflow (FR-14)

1. Jeder Inhalt trägt genau einen Workflow-Status; nur `Veröffentlicht` ist
   öffentlich sichtbar (Negativtest: Entwurf per URL nicht abrufbar).
2. Statuswechsel zu `Veröffentlicht` ist nur aus `Freigegeben` möglich;
   `Freigegeben` erfordert dokumentiertes Fachreview.
3. Gegeben ein Inhalt mit Marker `REVIEW ERFORDERLICH: Regulatorik`, dann
   ist der Wechsel zu `Freigegeben` technisch blockiert, bis ein
   Regulatorik-Review mit Ergebnis „freigegeben“ dokumentiert ist —
   ein Umgehungsversuch schlägt nachweisbar fehl.
4. Ein Inhalt mit `QUELLE ZU VERIFIZIEREN` kann nicht veröffentlicht werden
   (Build-/Workflow-Blocker mit klarer Fehlermeldung).
5. Zu jedem Review sind Person, Datum, Ergebnis und Kommentar
   nachvollziehbar (im MVP z. B. über Pull-Request-Historie — E5).

## AC-17 Suche (FR-15)

1. Eine Suche nach einem Begriff aus einer veröffentlichten Lektion
   (z. B. „Datenampel“) liefert diese Lektion in den Ergebnissen.
2. Ergebnisse zeigen Titel, Inhaltstyp, Kurs-/Modulzuordnung, Snippet und
   Free/Premium-Kennzeichnung.
3. Filter nach Rolle und Inhaltstyp schränken die Ergebnisliste korrekt ein.
4. Unveröffentlichte Inhalte erscheinen nie in Suchergebnissen
   (Negativtest mit Entwurfsinhalt).
5. Die Suche ist per Tastatur bedienbar; Ergebnisse werden Screenreadern
   als Liste mit Trefferzahl angekündigt.
6. Suchanfragen werden nicht personenbezogen protokolliert (höchstens
   aggregiert/anonym für die Suchqualität — Abgleich mit NFR-D).

## AC-18 Barrierefreiheit (NFR-A)

1. Automatisierte a11y-Prüfung (z. B. axe-core) über alle Seitentypen:
   0 Fehler der Kategorien „critical“ und „serious“ vor Launch.
2. Manueller Tastaturtest: Alle Kernflows (Registrierung, Lektion, Quiz,
   Simulation, Datenampel, Prompt-Werkstatt, Prüfung, Suche) sind ohne Maus
   vollständig durchführbar; der Fokus ist stets sichtbar.
3. Manueller Screenreader-Test (mind. ein Desktop- und ein Mobile-Reader)
   für dieselben Kernflows: Alle Inhalte und Zustandsänderungen
   (Quiz-Feedback, Fortschritt) werden angesagt.
4. Kein Inhalt und keine Übung ist nur über Farbe verständlich
   (Datenampel-Sondertest, AC-10.4); Kontraste erfüllen 4,5:1 für Text.
5. Bei 200 % Browser-Zoom bleiben alle Kernflows nutzbar (kein abgeschnittener
   Inhalt, keine blockierten Buttons).

## AC-19 Mobile Nutzung (NFR-B)

1. Alle Kernflows sind auf einem 360-px-Viewport vollständig nutzbar
   (manueller Gerätetest, mind. je ein Android- und ein iOS-Browser).
2. Kein horizontales Scrollen auf Inhaltsseiten; Tabellen und
   Prozesskarten sind mobil scroll- oder umbruchfähig aufbereitet.
3. Interaktionen (Quiz, Ampel, Simulation) haben Touch-Ziele von mindestens
   ~44 px und funktionieren ohne Hover.
4. Inhaltsseiten sind auf 4G in ≤ ~3 s interaktiv (Messverfahren gemäß
   NFR-C1, in Phase 2 präzisiert).

## AC-20 Datenschutz (NFR-D)

1. Das Datenmodell enthält nur die in FR-10.5/FR-16 definierten
   personenbezogenen Felder; jede Erweiterung erfordert dokumentierte
   Begründung (Datenschutz-Check im PR).
2. Es existiert keine Funktion, mit der Dritte individuelle Lernstände
   einsehen können (Code- und API-Review).
3. HTTPS ist erzwungen; Passwörter sind nach Stand der Technik gehasht;
   keine Secrets im Repository (automatisierter Secret-Scan im CI).
4. Ohne Einwilligung werden keine Analytics-/Tracking-Dienste geladen
   (Netzwerk-Audit der ausgelieferten Seiten); Umfang gemäß Entscheidung
   M-E3.
5. Datenauskunft und Kontolöschung sind durchführbar und einmal
   testweise vollzogen worden (Probelauf vor Launch).

## AC-21 Inhaltliche Abnahme des Pilotkurses

1. Alle 7 Module erfüllen die Inhalte-DoD aus `docs/definition-of-done.md`
   (inkl. Struktur, synthetische Daten, Marker, Transferaufgaben).
2. Modul 5 und der Zertifikatstext haben das Regulatorik-Review durchlaufen;
   alle Quellen sind verifiziert (kein `QUELLE ZU VERIFIZIEREN`).
3. Der Abschlussfall (Modul 7) deckt nachweislich fünf unterschiedliche
   Risikosituationen ab (Dateneingabe, Halluzination, Regulatorik,
   fehlender Kontrollpunkt, Kommunikation) und jede hat mindestens einen
   Fehlpfad mit erklärender Auswertung.
4. Mindestens 5 Testpersonen aus der Zielgruppe (verschiedene Rollen) haben
   den Kurs im Pilot durchlaufen; kritisches Feedback ist bewertet und
   adressiert oder begründet zurückgestellt.

---

## Abnahmeverfahren

1. **Feature-Abnahme:** je Funktionsbereich gegen AC-1 bis AC-20;
   Nachweise (Testprotokolle, Screenshots, Audit-Ergebnisse) werden
   dokumentiert.
2. **Inhaltliche Abnahme:** AC-21 durch Redaktion und Reviewer.
3. **Launch-Freigabe:** ausdrückliche Freigabe durch den Auftraggeber —
   kein Deployment ohne diese Freigabe (`CLAUDE.md`).
   **ENTSCHEIDUNG AUFTRAGGEBER:** Wer nimmt formal ab (eine Person oder
   Gremium Redaktion + Auftraggeber)?
