# Kostenschätzung — VersicherungsTech KI-Akademie (MVP und Wachstum)

**Status:** Entwurf (Teil der ADR-0002-Unterlagen)
**Stand:** 2026-07-15
**Grundlagen:** `docs/hosting-comparison.md` (belegte Preise mit Quellen
und Abrufdatum), `docs/operating-model-options.md`

**Wichtig:** Dies ist eine **Schätzung mit dokumentierten Annahmen**, keine
Angebotskalkulation. Belegte Listenpreise sind als solche gekennzeichnet
(Quellen in `docs/hosting-comparison.md`); wo Preise UNGEKLÄRT sind, werden
**Annahme-Korridore** verwendet und als `ANNAHME` markiert. Alle Beträge
**EUR netto pro Monat**, sofern nicht anders angegeben. Personalkosten für
Entwicklung sind nicht enthalten (nur Betriebszeit als Zeitangabe).

---

## 1. Lastmodell (Annahmen A-K1 bis A-K6)

Die Plattform ist textbasiert, lesedominiert, mit statisch generierten
Inhalten — der Ressourcenbedarf wächst deutlich langsamer als die
Nutzerzahl.

| # | Annahme | Wert |
|---|---|---|
| A-K1 | Monatlich aktive Nutzer (MAU) als Anteil der Registrierten | 40 % (junge Plattform; sinkt real über Zeit — konservativ) |
| A-K2 | Gleichzeitige aktive Sessions in der Spitze | ~1 % der MAU |
| A-K3 | Dynamische Requests (Auth, Fortschritt, Prüfung) pro aktiver Session | < 1 Request/Minute (Inhalte kommen statisch/cachebar) |
| A-K4 | Datenbankgröße | Minimal-Datenmodell: wenige KB je Nutzer → selbst bei 50.000 Registrierten « 5 GB inkl. Indizes |
| A-K5 | E-Mail-Volumen (Verifizierung, Reset; keine Werbung) | ≈ 1,5 E-Mails je Neuregistrierung + 0,1/Bestandsnutzer/Monat |
| A-K6 | Traffic | Textseiten klein (kein Video!); Egress bleibt in Free-/Pauschalgrenzen der Anbieter |

Abgeleitete Spitzenlast bei 50.000 Registrierten: ~20.000 MAU, ~200
gleichzeitige Sessions, < 10 dynamische Requests/Sekunde — **eine kleine
Node-App und eine kleine PostgreSQL tragen das problemlos**; Redundanz und
Backups treiben die Kosten, nicht die Last.

## 2. Szenario-Kosten je Betriebsmodell

### 2.1 Modell 2 — Scalingo (EU-PaaS) — Empfehlung aus ADR-0002

Belegte Preise (Abruf 2026-07-15): Container M 14,40 €, L 28,80 €,
XL 57,60 €; PostgreSQL Starter 512M 7,20 €. Business-PG: UNGEKLÄRT →
`ANNAHME`-Korridor 40–120 € je nach Stufe (vor Entscheidung verifizieren).

| Posten | MVP/Launch | 1.000 reg. | 10.000 reg. | 50.000 reg. |
|---|---|---|---|---|
| App-Container | 1× M = 14,40 | 2× M = 28,80 (Redundanz) | 2× L = 57,60 | 2–3× XL = 115–173 |
| PostgreSQL | Starter 512M = 7,20 | Starter 1G/2G ≈ 15–30 (`ANNAHME`) | Business (klein) ≈ 40–80 (`ANNAHME`) | Business (mittel) ≈ 80–150 (`ANNAHME`) |
| Review Apps (PR-Previews) | ≈ 5–15 (nutzungsabhängig, S/M-Container stundenweise, `ANNAHME`) | 5–15 | 10–25 | 10–25 |
| E-Mail (extern, s. 2.4) | 0–5 | ≈ 5 | ≈ 10–20 | ≈ 25–45 |
| Monitoring/Metriken | inklusive | inkl. | inkl. | inkl. |
| **Summe** | **≈ 30–40** | **≈ 55–80** | **≈ 120–185** | **≈ 230–395** |
| Eigene Betriebszeit | < 0,5 h/Monat | < 0,5 h | ~1 h | ~2 h |

### 2.2 Modell 1 — Hetzner (VM self-hosted) — kostengünstigste vertretbare Alternative

Belegte Preise (Abruf 2026-07-15): CX22 3,79 € (**Stand vor der
Preisanpassung zum 15.06.2026 — neue Listenpreise UNGEKLÄRT**; Korridor
`ANNAHME` +0–30 %); Backup-Option +20 % des Serverpreises; Object Storage
4,99 € (1 TB inkl.) für DB-Dump-Zweitsicherung.

| Posten | MVP/Launch | 1.000 reg. | 10.000 reg. | 50.000 reg. |
|---|---|---|---|---|
| VM(s) (App + PostgreSQL) | 1× CX22 ≈ 4–5 | 1× CX22 + Backup ≈ 5–6 | 2 VMs (App/DB getrennt) ≈ 10–14 | 2–3 größere VMs ≈ 25–40 (`ANNAHME`) |
| VM-Backups (20 %) | ≈ 1 | ≈ 1–2 | ≈ 2–3 | ≈ 5–8 |
| Object Storage (Dump-Zweitsicherung) | 4,99 | 4,99 | 4,99 | 4,99 |
| E-Mail (extern) | 0–5 | ≈ 5 | ≈ 10–20 | ≈ 25–45 |
| Monitoring (selbst betrieben) | 0 (auf App-VM) | 0 | ≈ 4 (eigene kleine VM) | ≈ 4–8 |
| **Summe Infrastruktur** | **≈ 10–16** | **≈ 16–23** | **≈ 31–46** | **≈ 64–106** |
| **Eigene Betriebszeit (der wahre Preis)** | **4–8 h/Monat** | 4–8 h | 6–10 h | 8–16 h |

Enthält: OS-/Docker-Patching, eigenes Postgres inkl. Backup-/Restore-Tests
(Pflicht laut §5.1/NFR-F2), TLS, Härtung, Preview-Deployments als Eigenbau
(z. B. Coolify). Bewertet man die Betriebszeit auch nur mit 100 €/h, ist
Modell 1 ab der ersten Stunde teurer als Modell 2.

### 2.3 Modell 3 — Scaleway (EU-Cloud + Managed PostgreSQL) — wartungsarme Alternative zu PaaS

Belegte Preise (Abruf 2026-07-15): PLAY2-PICO ab 0,014 €/h ≈ 10,20 €/Monat
(**Stand nach Preisänderung 01.06.2026 UNGEKLÄRT**); Object Storage
0,013 €/GB; Cockpit-Monitoring Free-Plan; TEM 300 Mails/Monat frei.
Managed-PostgreSQL-Preise UNGEKLÄRT → `ANNAHME`-Korridor 20–50 €
(kleinste Stufe ohne HA) bzw. 50–120 € (HA).

| Posten | MVP/Launch | 1.000 reg. | 10.000 reg. | 50.000 reg. |
|---|---|---|---|---|
| App (Instance oder Serverless Container) | ≈ 10–15 | ≈ 15–25 | ≈ 25–45 | ≈ 50–90 (`ANNAHME`) |
| Managed PostgreSQL | ≈ 20–50 (`ANNAHME`) | ≈ 20–50 | ≈ 50–120 (HA, `ANNAHME`) | ≈ 80–150 (`ANNAHME`) |
| E-Mail (TEM) | 0 (Free Tier) | ≈ 0–5 | ≈ 10–20 | ≈ 25–45 |
| Monitoring (Cockpit) | 0 (Free) | 0 | 0–29 | 29 (Premium, `ANNAHME`) |
| **Summe** | **≈ 30–65** | **≈ 35–80** | **≈ 85–215** | **≈ 185–315** |
| Eigene Betriebszeit | 1–3 h/Monat | 1–3 h | 2–4 h | 3–6 h |

### 2.4 Querschnittsposten (alle Modelle)

| Posten | Kosten | Beleg/Annahme |
|---|---|---|
| Transaktions-E-Mail | MVP: 0–5 €; 50k: ≈ 25–45 € | Scaleway TEM belegt: 300/Monat frei; Scale-Plan 100k inkl., dann 0,20 €/1.000 (Monatspreis Scale: UNGEKLÄRT). Volumen: A-K5 → 50k reg. ≈ 2.000 Neureg./Monat ≈ 8.000 Mails (`ANNAHME`) |
| Domain/DNS (Subdomain unter versicherungstech-magazin.de) | ≈ 0 (vorhandene Domain) | `ANNAHME`: DNS beim bestehenden Domain-Anbieter |
| Git-Hosting + CI | 0 € (GitHub Free für private Repos, 2.000 CI-Minuten/Monat) bis ≈ 4 €/Nutzer (Team) | `ANNAHME`; CI-Bedarf der Content-Builds klein; QUELLE ZU VERIFIZIEREN (GitHub-Preise nicht Teil der Recherche) |
| TLS-Zertifikate | 0 € (Let's Encrypt bzw. PaaS-inklusive) | Standard |
| Suchtechnik | 0 € im Build-Index-Fall; selbst gehostete Engine ≈ +5–15 € | Entscheidung erst ADR-0004 (nach Content-Schemata) |

## 3. Vergleich der Modelle (Gesamtsicht, Monatskosten netto)

| Szenario | M1 Hetzner (nur Infra) | M1 inkl. Betriebszeit à 100 €/h | M2 Scalingo | M3 Scaleway |
|---|---|---|---|---|
| MVP | 10–16 € | 410–816 € | 30–40 € | 30–65 € |
| 1.000 | 16–23 € | 416–823 € | 55–80 € | 35–80 € |
| 10.000 | 31–46 € | 631–1.046 € | 120–185 € | 85–215 € |
| 50.000 | 64–106 € | 864–1.706 € | 230–395 € | 185–315 € |

**Kernaussage:** Die Infrastrukturkosten sind in jedem Modell und jedem
Szenario klein gegenüber Content-Produktion und Entwicklung. Die
Entscheidung sollte über Betriebsverantwortung und Datenschutz-Papierlage
fallen, nicht über die Differenz von 100–300 €/Monat.

## 4. Annahmen der Kostenschätzung (Zusammenfassung)

1. Lastmodell A-K1 bis A-K6 (Abschnitt 1) — insbesondere: lesedominiert,
   statische Inhalte, Minimal-Datenmodell, kein Video.
2. Preisstand: belegte Listenpreise mit Abrufdatum 2026-07-15; **Hetzner-
   Preise vor der Anpassung vom 15.06.2026 und Scaleway-Preise vor der
   Änderung vom 01.06.2026 sind möglicherweise überholt** (UNGEKLÄRT,
   Korridore verwenden Aufschläge).
3. UNGEKLÄRT-Preise (Scalingo Business-PG, Scaleway Managed PG,
   OVH/IONOS/STACKIT generell) sind als `ANNAHME`-Korridore aus
   vergleichbaren Marktprodukten geschätzt und **vor Vertragsschluss zu
   verifizieren** (H5 in `docs/hosting-comparison.md`).
4. Keine Bezahlstrecke im MVP (E2a) → keine Zahlungsanbieter-Gebühren
   enthalten; bei Ausbaustufe 1 kommen transaktionsabhängige Gebühren des
   Zahlungsanbieters hinzu (separat zu kalkulieren).
5. Betriebszeit-Bewertung mit 100 €/h ist eine Rechenhilfe zur
   Vergleichbarkeit, kein Angebot.
6. Wechselkurse irrelevant (alle relevanten Preise in EUR; OVH-USD-Belege
   nicht verwendet).
7. Keine Rabatte/Committed-Use berücksichtigt.

## 5. Kostenrisiken

| Risiko | Wirkung | Umgang |
|---|---|---|
| UNGEKLÄRT-Preise fallen höher aus als Korridor | +50–100 €/Monat möglich | H5-Verifikation vor Vertragsschluss; Budgetpuffer |
| Review-Apps-Nutzung stärker als angenommen | +10–30 €/Monat | Auto-Destroy bei PR-Close (Scalingo-Standard) |
| E-Mail-Volumen (Passwort-Resets) höher | gering (0,20 €/1.000) | beobachten |
| Traffic-Spitzen durch Magazin-Verlinkung | gering (statisch/cachebar) | CDN-Cache; kein Video hilft strukturell |
| Preisänderungen der Anbieter (2026 bereits zwei belegt) | mittel | Portabilität als Kriterium in ADR-0002; Container-Artefakt bleibt anbieterneutral |
