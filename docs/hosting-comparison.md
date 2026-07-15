# Hosting-Vergleich — VersicherungsTech KI-Akademie (MVP)

**Status:** Entwurf zur Entscheidung (Teil der ADR-0002-Unterlagen)
**Stand:** 2026-07-15 · Abrufdatum aller Quellen: **2026-07-15**
**Grundlagen:** ADR-0001 (Accepted), `docs/operating-model-options.md`

**Methodik und Beleglage:** Alle Angaben stammen von offiziellen
Anbieterquellen (Produktseiten, Doku, Rechtsdokumente/PDFs). Direkte
Seitenabrufe waren in der Rechercheumgebung teilweise durch einen
Netzwerk-Proxy blockiert; betroffene Angaben beruhen auf domainbeschränkten
Suchauszügen der offiziellen Seiten und sind **vor Vertragsschluss gegen
die Live-Seiten zu verifizieren**. Nicht Belegbares ist als **UNGEKLÄRT**
markiert. **Dieses Dokument enthält keine juristische Bewertung und
simuliert keine datenschutzrechtliche Anbieterfreigabe** — die
Prüfung von AVV, Subprozessoren und Drittlandbezügen obliegt der
juristischen Prüfung vor Vertragsschluss (Rolle: Legal/Regulatory Reviewer
+ Privacy/Security Reviewer).

Geprüfte Anbieter je Betriebsmodell (`docs/operating-model-options.md`):

- **Modell 1 (VM self-hosted):** Hetzner, IONOS, STACKIT
- **Modell 2 (EU-PaaS):** Scalingo, Clever Cloud
- **Modell 3 (EU-Cloud + Managed PostgreSQL):** Scaleway, OVHcloud
  (IONOS/STACKIT bieten ebenfalls Managed PostgreSQL)
- Zusätzlich betrachtet und **nicht präferiert:** Vercel (US-Vertragspartei,
  siehe Abschnitt 4)

---

## 1. Rechts- und Datenschutz-Steckbriefe

Ausdrücklich getrennt ausgewiesen: Unternehmenssitz ≠ Vertragspartei ≠
Serverstandort ≠ Datenstandort-Zusage ≠ Supportzugriff ≠ Logspeicherung ≠
Backups ≠ Subprozessoren.

### 1.1 Hetzner

| Dimension | Befund (Quellen: hetzner.com/docs.hetzner.com, Abruf 2026-07-15) |
|---|---|
| Unternehmenssitz | Hetzner Online GmbH, Gunzenhausen (DE), HRB 6089 Ansbach |
| Vertragspartei (DE) | Hetzner Online GmbH (laut AGB) |
| Serverstandorte | Nürnberg, Falkenstein (DE), Helsinki (FI); Cloud zusätzlich USA (Ashburn, Hillsboro), Singapur — Standortwahl je Ressource |
| Datenstandort | Speicherort folgt gewähltem Produktstandort; Hetzner-eigene Bestandsdaten ausschließlich EU. Vertragliche „Region-Lock“-Zusage darüber hinaus: UNGEKLÄRT |
| AVV/DPA | Ja; online im Kundenkonto abschließbar (accounts.hetzner.com/account/dpa; DPA-PDFs öffentlich) |
| Subprozessoren | Öffentliche PDF-Liste; enthält Nicht-EU-Firmen für die US-Standorte (Hetzner US LLC, NTT Global Data Centers Americas, QTS Hillsboro); bei Nutzung nur deutscher Standorte relevanter Anteil: juristisch zu prüfen |
| Supportzugriff | Support-Team laut Anbieter in Deutschland; Hetzner Finland Oy für technischen Support (FI/EU). Detaillierte Zugriffsorte: UNGEKLÄRT |
| Logspeicherung (Anbieter) | Logfiles max. 30 Tage; IP-Anonymisierung laut Datenschutzerklärung |
| Backups (Produkt) | Cloud-Backups: 20 % Aufschlag auf Serverpreis, 7 Slots (belegt); Snapshots pro GB (Preis UNGEKLÄRT) |
| Zertifizierungen | ISO/IEC 27001:2022 (Nürnberg, Falkenstein, Helsinki; gültig bis 09/2028). C5: nicht belegt (UNGEKLÄRT) |
| Managed PostgreSQL | **Existiert nicht** als eigenständiges DBaaS-Produkt (nur Managed-Server-/Webhosting-Kontexte) — für Modell 3 ungeeignet |
| Preisbesonderheit | **Preisanpassung + Produktstandardisierung zum 15.06.2026 für Neubestellungen** — neue Listenpreise UNGEKLÄRT; ältester Beleg CX22 (2 vCPU/4 GB): 3,79 €/Monat (netto/brutto UNGEKLÄRT); Object Storage 4,99 €/Monat netto (1 TB inkl.) |

### 1.2 IONOS

| Dimension | Befund (Quellen: ionos.de/cloud.ionos.com/ionos-group.com, Abruf 2026-07-15) |
|---|---|
| Unternehmenssitz | IONOS SE, Montabaur (DE); Konzern: IONOS Group SE |
| Vertragspartei (DE) | IONOS SE (für ionos.de-Produkte inkl. AVV); für „IONOS Cloud“ (Enterprise): vermutlich ebenfalls IONOS SE — UNGEKLÄRT |
| Serverstandorte | DE: Frankfurt (neues Cloud-RZ), Berlin; EU: Paris, Logroño (ES); UK, USA — Standortwahl produktabhängig |
| Datenstandort | Anbieterbotschaften „Datensouveränität“, RZ-Wahl möglich; generelle Region-Lock-Zusage: UNGEKLÄRT |
| AVV/DPA | Ja, kostenlos; seit 07/2022 Bestandteil der AGB (kein separater Abschluss nötig) |
| Subprozessoren | In AVV-Anlage 2 geführt; konkrete Namen/Nicht-EU-Anteile: UNGEKLÄRT |
| Supportzugriff | UNGEKLÄRT (keine offizielle Aussage gefunden) |
| Logspeicherung (Anbieter) | Webhosting: 8 Wochen (belegt); VPS/Cloud: UNGEKLÄRT |
| Backups (Produkt) | IONOS Cloud Backup Service ohne Lizenzgebühr (Details/Preise UNGEKLÄRT) |
| Zertifizierungen | ISO 27001 auf Basis IT-Grundschutz (BSI); **C5-Testat** (Compute Engine, Cloud Cubes, S3 Object Storage; Datum QUELLE ZU VERIFIZIEREN); SOC 1–3 (Frankfurt) |
| Managed PostgreSQL | **Ja** — IONOS Cloud DBaaS PostgreSQL (tägliche Backups, PITR 7 Tage, SLA 99,95 %); Preise nur über Preisrechner: UNGEKLÄRT |
| Kleine VMs | VPS M (2 Cores/2 GB/80 GB): 5 €/Monat laut Newsroom (netto/brutto UNGEKLÄRT) |

### 1.3 STACKIT

| Dimension | Befund (Quellen: stackit.de/docs.stackit.cloud, Abruf 2026-07-15) |
|---|---|
| Unternehmenssitz | STACKIT GmbH & Co. KG, Neckarsulm (DE); Schwarz Gruppe |
| Vertragspartei (DE) | STACKIT GmbH & Co. KG |
| Serverstandorte | **Ausschließlich DE (eu01, Raum Heilbronn) und AT (eu02)** |
| Datenstandort | Anbieterzusage: Betrieb aller Services ausschließlich in DE/AT; vertragliche Region-Lock-Klausel: UNGEKLÄRT |
| AVV/DPA | Ja, öffentlich als PDF; Abschlussmechanik: UNGEKLÄRT |
| Subprozessoren | Öffentliche namentliche Liste **nicht gefunden** (UNGEKLÄRT; vermutlich AVV-Anlage) |
| Supportzugriff | UNGEKLÄRT |
| Logspeicherung (Anbieter) | UNGEKLÄRT |
| Backups (Produkt) | Backup Storage, Server Backup Management, Snapshots vorhanden; Preise UNGEKLÄRT |
| Zertifizierungen | C5 Typ 2, ISO 27001, ISAE 3000 (SOC 2), ISAE 3402 (laut Anbieter) |
| Managed PostgreSQL | **Ja** — PostgreSQL Flex (3 Replikate, automatische Backups/Patches); Preise nur über Calculator/Preisliste: UNGEKLÄRT |
| Anmerkung | Enterprise-orientiert; Self-Service-Preistransparenz am geringsten unter den geprüften Anbietern |

### 1.4 Scalingo (EU-PaaS)

| Dimension | Befund (Quellen: scalingo.com/doc.scalingo.com, Abruf 2026-07-15) |
|---|---|
| Unternehmenssitz | Scalingo SAS, Straßburg (FR), RCS 808 665 483 |
| Vertragspartei (DE) | Scalingo SAS (keine deutsche Entität gefunden) |
| Infrastruktur/Serverstandort | Keine eigenen RZ; läuft auf **3DS Outscale** (Dassault-Tochter), Region osc-fr1 = Paris/Umland (FR); SecNumCloud-Region osc-secnum-fr1 auf Anfrage. **Keine DE-Region** |
| Datenstandort | „All data is hosted in France within 3DS Outscale datacenters“ (Anbieterzusage) |
| AVV/DPA | Ja (scalingo.com/data-processing-agreement) |
| Subprozessoren | Liste laut Doku im DPA geführt; konkrete Namen/Nicht-EU-Anteile: UNGEKLÄRT (DPA-Volltext prüfen; Infrastruktur-Subprozessor Outscale ist FR) |
| Supportzugriff | Admin-Zugriff „authorized personnel only“, 2FA, Bastion, Access-Reviews (Sicherheitsdoku); Bedingungen für Supportzugriff auf Kundendaten: UNGEKLÄRT |
| Logspeicherung | Log-Archive „unlimited“ als Feature; Aufbewahrungsdauer der Plattform-eigenen Logs: UNGEKLÄRT |
| Backups (Produkt) | PostgreSQL: tägliche Backups, 7 Tage Aufbewahrung (Starter); Business: bis 50 Backups + PITR (7–30 Tage je Klasse) — belegt |
| Zertifizierungen | ISO 27001:2022 (seit 2022), HDS; SecNumCloud selbst nicht (angestrebt), IaaS-Unterbau Outscale ist SecNumCloud-qualifiziert |
| Preise (belegt, netto) | Container M (512 MB): 14,40 €/M; L (1 GB): 28,80 €/M; XL (2 GB): 57,60 €/M; PostgreSQL Starter 512M: 7,20 €/M; Business-Pläne: UNGEKLÄRT |
| Besonderheit | **Review Apps pro Pull Request eingebaut** (GitHub/GitLab, Auto-Create/Destroy) — deckt Preview-Deployments nativ ab; Metriken + Alerts inklusive |

### 1.5 Clever Cloud (EU-PaaS)

| Dimension | Befund (Quellen: clever-cloud.com/developers.clever-cloud.com, Abruf 2026-07-15) |
|---|---|
| Unternehmenssitz | Clever Cloud SAS, Nantes (FR), RCS B 524 172 699 |
| Vertragspartei (DE) | Clever Cloud SAS |
| Infrastruktur/Serverstandort | Eigene Hardware in Partner-RZ: Paris (mehrere Standorte), Roubaix (auf OVHcloud), Gravelines; EU außerhalb FR: Warschau; Nicht-EU-Zonen existieren (Montreal, Singapur, Sydney) — Kunde wählt Zone |
| Datenstandort | Zonen-Wahl durch Kunden, Default Frankreich; Zusage bezieht sich auf gewählte Zone |
| AVV/DPA | Ja (in GTC inkorporiert; SCC-Verweis) |
| Subprozessoren | Öffentliche PDF-Liste (Version 2026/02); Inhalt: UNGEKLÄRT; Partner-Infrastrukturen belegt: OVHcloud, Scaleway, Cloud Temple, IONOS |
| Supportzugriff | UNGEKLÄRT |
| Logspeicherung | Anwendungslogs 7 Tage (belegt) |
| Backups (Produkt) | PostgreSQL: tägliche Backups, 7 Tage Aufbewahrung (anpassbar per Support) |
| Zertifizierungen | ISO 27001:2022, HDS (alle 6 Aktivitäten); SecNumCloud nicht (über Cloud Temple angeboten) |
| Preise | Instanz-Preisliste zuletzt offiziell belegbar mit Stand 08/2023 (XS 1 vCPU/1 GiB: 16 €/M; S 2 vCPU/2 GiB: 32 €/M) — **Aktualität UNGEKLÄRT**; PostgreSQL-Planpreise: UNGEKLÄRT |
| Preview-Deployments | Über offizielle GitHub Action (Review-Apps pro PR); kein in die Plattform eingebautes Feature wie bei Scalingo |

### 1.6 Scaleway (EU-Cloud + Managed PostgreSQL)

| Dimension | Befund (Quellen: scaleway.com, Abruf 2026-07-15) |
|---|---|
| Unternehmenssitz | Scaleway S.A.S., Paris (FR); iliad-Gruppe |
| Vertragspartei (DE) | Scaleway S.A.S. (französisches Recht; maßgebliche Vertragssprache Französisch) |
| Serverstandorte | Paris (fr-par), Amsterdam (nl-ams), Warschau (pl-waw), Mailand — **kein DE-Standort** |
| Datenstandort | Anbieteraussage „100 % europäische Jurisdiktion“. **Produktspezifisch relevant: Managed-Database-Backups werden standardmäßig cross-region gespeichert** (z. B. Paris→Amsterdam; bleibt EU) |
| AVV/DPA | Ja, öffentlich (DPA-Version 06/2024) + SCC-Dokumente |
| Subprozessoren | Öffentliche Liste + Änderungshistorie (u. a. Digital Realty, AtNorth); vollständiger aktueller Inhalt/Nicht-EU-Anteile: UNGEKLÄRT |
| Supportzugriff | „France-based in-house technical support teams, 24/7“ (Anbieteraussage); exklusiver EU-Zugriff: UNGEKLÄRT |
| Logspeicherung | Verbindungsdaten laut Privacy Policy; Fristen: UNGEKLÄRT |
| Backups (Produkt) | Managed DB: Auto-Backup 1×/Tag, 7 Tage, konfigurierbar (belegt; cross-region s. o.) |
| Zertifizierungen | ISO/IEC 27001:2022 (bis 12/2026), HDS; SecNumCloud im Qualifizierungsprozess; C5: UNGEKLÄRT/nicht belegt |
| Preise (teils belegt, netto) | PLAY2-PICO (1 vCPU/2 GB): ab 0,014 €/h (~10 €/M) — Stand nach Preisänderung 01.06.2026: UNGEKLÄRT; Object Storage 0,013 €/GB/M; Cockpit-Monitoring: Free-Plan (Metriken 31 T/Logs 7 T); **Transactional Email (TEM)** vorhanden (300 Mails/M frei; Scale: 100k inkl., dann 0,20 €/1.000); Managed-PostgreSQL-Preise: UNGEKLÄRT |
| Preisbesonderheit | Preisänderungen zum **01.06.2026** angekündigt — alle älteren Preisangaben prüfen |

### 1.7 OVHcloud (EU-Cloud + Managed PostgreSQL)

| Dimension | Befund (Quellen: ovhcloud.com/ovh.de, Abruf 2026-07-15) |
|---|---|
| Unternehmenssitz | OVH Groupe SA, Roubaix (FR), börsennotiert; operative OVH SAS |
| Vertragspartei (DE) | **OVH GmbH, Saarbrücken** laut AGB-PDFs auf ovh.de; tagesaktuelle Bestätigung für Neuverträge: UNGEKLÄRT |
| Serverstandorte | FR: Gravelines, Roubaix, Straßburg; **DE: Limburg bei Frankfurt**; PL: Warschau; weitere weltweit — Kunde wählt |
| Datenstandort | Lokalisierungswahl; „EU Trusted Zone“-Option (Hosting + Verarbeitung ausschließlich EU) |
| AVV/DPA | Ja; deutscher AVV als PDF (inkl. Zustimmungserfordernis für Subprozessoren außerhalb der OVH-Gruppe) |
| Subprozessoren | Öffentliche PDF-Listen (Unterauftragsverarbeiter + verbundene Unternehmen). **Belegt: Aiven Oy (FI/EU) als Subprozessor für Betrieb der Managed Databases**; Nicht-EWR-Konzerngesellschaften per SCC möglich (z. B. Support) |
| Supportzugriff | Standard-/Business-/Premium-Support: Zugriffsorte UNGEKLÄRT; nur Enterprise-Support bietet auf Anfrage EU-only-Eingriffe |
| Logspeicherung | System-/Zugriffslogs **12 Monate** (belegt) |
| Backups (Produkt) | Managed PostgreSQL: Essential = tägliches Backup, 2 Tage Aufbewahrung; Business = 14 Tage (belegt) |
| Zertifizierungen | ISO 27001/17/18/701; **BSI C5** (Scope UNGEKLÄRT); SecNumCloud (Hosted Private Cloud); HDS; KRITIS-registriert in DE |
| Preise | EUR-Preise der kleinen Instances, Managed PostgreSQL, Load Balancer: UNGEKLÄRT (nur USD-Belege der US-Seite gefunden); Object Storage: keine Ingress-/Egress-/API-Gebühren (belegt), €-Satz UNGEKLÄRT |
| Anmerkung | Kein dediziertes Transaktions-E-Mail-Produkt auffindbar (Negativbeweis UNGEKLÄRT) |

## 2. Bewertung gegen die Projektkriterien

Skala: ++ / + / o / − / ? (= wesentliche Angaben UNGEKLÄRT). Bezogen auf
den ADR-0001-Zuschnitt (Node-App-Container + PostgreSQL + statische
Inhalte).

| Kriterium | Hetzner | IONOS | STACKIT | **Scalingo** | Clever Cloud | Scaleway | OVHcloud |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| EU-Datenstandort | ++ (DE wählbar) | ++ (DE wählbar) | ++ (nur DE/AT) | ++ (FR) | + (FR, Zonenwahl) | + (FR/NL/PL, DB-Backups cross-region) | ++ (DE wählbar) |
| AVV verfügbar/zugänglich | ++ | ++ | + | + | + | + | ++ (deutscher AVV) |
| Subprozessoren-Transparenz | + (öffentl. Liste, US-Anteile für US-Standorte) | ? | ? (keine öffentl. Liste gefunden) | ? (im DPA) | + (öffentl. PDF, Inhalt ungeprüft) | + (öffentl. Liste + Historie) | + (öffentl. Listen; Aiven Oy belegt) |
| Supportzugriff dokumentiert | + | ? | ? | o | ? | o | − (EU-only nur Enterprise) |
| Managed PostgreSQL | − (existiert nicht) | + (Preise ?) | + (Preise ?) | ++ (Preise Starter belegt) | + (Preise ?) | + (Backups belegt, Preise ?) | + (Backups belegt, Preise ?) |
| Backups eingebaut | o (20 % Aufschlag, VM-Ebene) | + | + | ++ (DB täglich, PITR Business) | + | + | + |
| Preview-Deployments | − (Eigenbau/Coolify) | − | − | **++ (Review Apps nativ)** | + (GitHub Action) | − | − |
| Monitoring eingebaut | − (Selbstbau; Prometheus-App) | + | + | + (Metriken/Alerts inkl.) | + (Grafana inkl., Alerting ?) | + (Cockpit Free) | + (Preise ?) |
| Wartungsaufwand | −− | − | − | ++ | ++ | o | o |
| Preistransparenz (Self-Service) | + (Anpassung 06/2026 ?) | − | − | ++ | − (Stand 2023) | o | − |
| Erwartete MVP-Kosten | ++ (am niedrigsten) | ? | ? | + | ? | + | ? |
| Vendor Lock-in / Portabilität | ++ | + | + | + (Buildpacks/Container, Standard-PG) | + | + | + |
| Zertifizierungstiefe (DE-relevant) | + (ISO) | ++ (ISO+C5) | ++ (ISO+C5 Typ 2) | + (ISO+HDS) | + (ISO+HDS) | + (ISO+HDS) | ++ (ISO+C5+SecNumCloud) |
| SSO-Fähigkeit der Plattform (für unsere App irrelevant — Auth liegt in der App) | n/a | n/a | n/a | n/a | n/a | n/a | n/a |

## 3. Zwischenfazit für ADR-0002

1. **Scalingo** ist die beste Passung für den MVP: einziger Anbieter mit
   nativ eingebauten Review-Apps (direkter Gewinn für den Git-Review-
   Workflow E5), belegten transparenten Preisen, Managed PostgreSQL mit
   dokumentierter Backup-Policy, ISO 27001 + HDS, rein französischer
   Infrastruktur (Outscale). Offene Prüfpunkte: DPA-Subprozessorenliste,
   Log-Fristen, Supportzugriffs-Bedingungen, Business-PG-Preise.
2. **Scaleway** ist die beste Modell-3-Alternative (Managed PG + TEM als
   E-Mail-Kandidat aus einer Hand); Achtung: DB-Backup-Cross-Region
   (EU-intern) und Preisstand nach 01.06.2026 prüfen.
3. **Hetzner** ist die kostengünstigste vertretbare Basis (Modell 1,
   deutsche Standorte, einfache AVV-Lage) — um den Preis des vollen
   Eigenbetriebs inkl. selbst verwaltetem PostgreSQL (kein DBaaS im
   Angebot) und der offenen Frage der neuen Listenpreise (15.06.2026).
4. **OVHcloud** bietet als einziger die Kombination deutsche Vertragspartei
   (laut AGB-PDFs) + deutscher Serverstandort + C5, hat aber die
   schwächste Preistransparenz, 12-Monats-Anbieterlogs und den
   Aiven-Subprozessor bei Managed DB — als Kandidat für eine spätere
   „maximale DE-Compliance“-Anforderung notiert.
5. **IONOS/STACKIT** scheiden für den MVP wegen geringer
   Self-Service-Preistransparenz und ungeklärter Basisinformationen aus
   (bleiben Kandidaten für spätere B2B-/Compliance-Anforderungen).
6. **Clever Cloud** ist ein valider Scalingo-Ersatz; Preisbeleglage
   (Stand 2023) derzeit zu unsicher für eine Empfehlung.

## 4. Vercel (betrachtet, nicht präferiert)

Vercel Inc. (USA, Sitz San Francisco laut vercel.com/about; Recht
Kalifornien laut Terms) bietet ein öffentliches DPA (auch für Pro-Pläne)
mit EU-Standardvertragsklauseln und konfigurierbare EU-Function-Regionen
(u. a. Frankfurt `fra1`). Eine vollständige EU-Datenresidenz über alle
Dienste (Logs, Builds, Analytics) ist offiziell **nicht belegt
(UNGEKLÄRT)**. Quellen: vercel.com/legal/dpa, vercel.com/docs/regions,
vercel.com/docs/functions/configuring-functions/region (Abruf 2026-07-15).
Wegen US-Vertragspartei und Drittlandtransfer-Komplexität gegenüber
gleichwertigen EU-Optionen für dieses Projekt nicht weiterverfolgt —
keine juristische Bewertung, sondern Priorisierungsentscheidung.

## 5. Offene Datenschutz- und Vertragsfragen (vor Vertragsschluss zu klären)

| # | Punkt | Betroffen |
|---|---|---|
| H1 | DPA-Volltext + Subprozessorenliste des gewählten Anbieters juristisch prüfen (Nicht-EU-Anteile?) | Scalingo (primär), alle |
| H2 | Supportzugriffs-Bedingungen (von wo, unter welchen Kontrollen) schriftlich klären | Scalingo, Scaleway, IONOS, STACKIT, OVH (Nicht-Enterprise) |
| H3 | Log-Aufbewahrungsfristen des Anbieters vs. eigenes Löschkonzept (§5.1: ≤ 14 Tage eigene Sicherheitslogs) abgleichen | Scalingo (?), OVH (12 Monate Anbieterlogs), alle |
| H4 | Backup-Speicherorte (Scaleway: cross-region) und Backup-Verschlüsselung bestätigen | Scaleway, Scalingo, alle |
| H5 | Live-Preise verifizieren (Hetzner-Anpassung 15.06.2026; Scaleway-Anpassung 01.06.2026; Clever-Cloud-Preisstand 2023) | Kostenschätzung |
| H6 | Vertragspartei OVH GmbH für Neuverträge tagesaktuell bestätigen (falls OVH gewählt) | OVHcloud |
| H7 | E-Mail-Versand: Anbieterwahl (Kandidat Scaleway TEM; Alternativen zu prüfen) + AVV | F4/DF4 |

**Keine dieser Prüfungen ist mit diesem Dokument erledigt oder
vorweggenommen.**
