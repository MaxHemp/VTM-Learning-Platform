# ADR-0002: Web-Framework, Hosting, PostgreSQL und Deployment

**Status:** **Accepted** (bestätigt durch den Auftraggeber am 2026-07-15,
mit Festlegungen — siehe Abschnitt „Bestätigung durch den Auftraggeber").
**Wichtig:** Die Architektur ist **technisch akzeptiert**; die Anbieter
sind **rechtlich/datenschutzrechtlich noch nicht freigegeben**. Kein
Hostingvertrag geschlossen, kein Deployment-Prozess aktiviert, keine
Implementierung begonnen.
**Datum:** 2026-07-15 (vorgeschlagen und angenommen)
**Entscheider:** Auftraggeber (VersicherungsTech Magazin) auf Vorschlag
der Entwicklung
**Referenzen:** `docs/framework-comparison.md`,
`docs/hosting-comparison.md`, `docs/operating-model-options.md`,
`docs/cost-estimate.md`, ADR-0001 (Accepted),
`docs/threat-model-initial.md`

## Kontext

ADR-0001 (Accepted) legt fest: Git-basierte, schemavalidierte Inhalte;
statische Generierung mit kleiner Server-Schicht; PostgreSQL mit
Minimal-Nutzerdatenmodell; CI-erzwungene Publikations-Gates; EU-Hosting;
Deployment nur nach ausdrücklicher Freigabe. Offen sind die konkreten
Bausteine: Web-Framework, Hosting-Anbieter/Betriebsmodell,
PostgreSQL-Betrieb und Deployment-Weg.

Vier Frameworks (Next.js, Astro, SvelteKit, Nuxt) und sieben EU-Anbieter
in vier Betriebsmodellen wurden anhand offizieller Quellen verglichen
(Abrufdatum 2026-07-15; Beleglage und UNGEKLÄRT-Markierungen in den
referenzierten Dokumenten). Vorgabe des Auftraggebers: Content-Schemata
werden erst mit ADR-0003 finalisiert; die Suchtechnik wird erst danach
entschieden (ADR-0004) — dieses ADR hält beide Wege offen.

## Entscheidung (vorgeschlagen)

### 1. Web-Framework: **Astro** mit Node-Adapter und Svelte-Islands

- **Astro** (v7, MIT) als Framework: Content Collections mit
  Zod-Schema-Validierung setzen die ADR-0001-Kernanforderung
  (schemavalidierte deklarative Inhalte mit Build-Gates) als stabiles
  Kern-Feature um; offizielle MDX-Integration; On-demand Rendering für
  die App-Routen; eingebautes i18n-Routing (Mehrsprachigkeit technisch
  vorbereitet, MVP Deutsch).
- **`@astrojs/node`-Adapter** (Standalone) — die Anwendung wird als
  gewöhnlicher Node.js-Container gebaut und ist damit anbieterneutral.
- **Svelte als Island-Framework** für die interaktiven Übungskomponenten
  (Quiz, Simulation, Datenampel, Prompt-Bausatz): Compiler-a11y-Warnungen
  unterstützen die AC-18-Pflichten; minimale Bundles auf Leseseiten.
  (Austauschbar gegen Preact/React ohne Architekturfolge.)
- **Sessions/Auth:** Astros stabile Sessions-API + eigene schmale
  Auth-Schicht (E-Mail/Passwort, Argon2id, serverseitige Sessions) gemäß
  Threat Model T1–T2; SSO/OIDC später als zusätzlicher Anmeldeweg
  andockbar (Auth-Bibliothek-Wahl ist Implementierungsdetail, kein ADR).

### 2. Betriebsmodell und Hosting: **EU-PaaS Scalingo** (Region osc-fr1, Paris)

- **App:** Scalingo-Container (Start: 1× M, Launch: 2× M für Redundanz);
  Node.js-Buildpack oder Container-Deployment.
- **PostgreSQL:** Scalingo Managed PostgreSQL — Start mit Starter-Plan,
  **vor Launch Wechsel auf Business-Plan** (Multi-Node, PITR, bis 50
  Backups) für die Produktionsdatenbank.
- **Preview-Deployments:** Scalingo **Review Apps** — automatische App pro
  Pull Request, Auto-Destroy bei Close; erfüllt die
  Preview-Anforderung des Git-Review-Workflows nativ.
- **Begründung der Anbieterwahl** (Details: `docs/hosting-comparison.md`):
  französische Vertragspartei (SAS) mit EU-Infrastruktur (3DS Outscale,
  Paris), ISO 27001 + HDS, transparente belegte Preise, eingebaute
  Review-Apps/Metriken/Alerts, dokumentierte Backup-Policy — bei
  minimalem Betriebsaufwand für ein kleines Team (Modell-2-Bewertung in
  `docs/operating-model-options.md`).
- **Zweitsicherung (Backups):** täglicher logischer DB-Dump (pg_dump) aus
  der Plattform heraus in einen **verschlüsselten Bucket eines zweiten
  EU-Anbieters** (Kandidat: Hetzner Object Storage, DE, 4,99 €/Monat) —
  entkoppelt die Wiederherstellbarkeit vom PaaS-Anbieter
  (Threat Model T21, NFR-F2; Aufbewahrung ≤ 30 Tage gemäß §5.1).
- **E-Mail (Transaktion):** Kandidat Scaleway TEM (FR, Free Tier, belegte
  Staffelpreise); finale Anbieterwahl inkl. AVV = separater Prüfpunkt H7,
  **nicht Teil dieses ADR**.

### 3. Deployment-Weg (Prozess, noch nicht aktiviert)

1. GitHub-Repository (bestehend) + GitHub Actions als CI: Schema-Gates,
   Marker-Gates, Tests, a11y-Checks, Secret-Scan, Build.
2. Pull Request → Scalingo Review App (Vorschau für Redaktion/Review).
3. Merge auf Hauptbranch → Build + Staging-Deployment.
4. **Produktions-Deployment ausschließlich nach ausdrücklicher Freigabe
   des Auftraggebers** (manueller Approval-Schritt; geschützte Umgebung —
   Threat Model T18). Diese Pipeline wird erst nach Freigabe dieses ADR
   und der Implementierungsphase eingerichtet.

## Betrachtete Alternativen

### Frameworks (Details: `docs/framework-comparison.md`)
- **SvelteKit** (Zweitplatzierter): beste eingebaute Barrierefreiheit,
  unabhängigste Governance; abgelehnt, weil Content-Schema-Validierung und
  MDX-Äquivalent Eigenbau wären — das Kernstück der Architektur bekäme
  die schwächste Werkzeugunterstützung. Bleibt Rückfalloption.
- **Next.js:** abgelehnt für diesen Zuschnitt: keine eingebaute
  Content-Validierung, dokumentierte Self-Hosting-Caveats, stärkste
  Anbieterkopplung (Vercel), mehr Laufzeitkomplexität als der Anwendungsfall
  braucht.
- **Nuxt:** solide, aber MDC statt MDX, Schema-Details UNGEKLÄRT, keine
  Vorteile gegenüber Astro für eine content-first-Plattform.

### Hosting/Betrieb (Details: `docs/hosting-comparison.md`, `docs/operating-model-options.md`, `docs/cost-estimate.md`)
- **Hetzner VM self-hosted (Modell 1)** — *kostengünstigste vertretbare
  Alternative* (10–16 €/Monat MVP): abgelehnt als Primärweg wegen vollem
  Eigenbetrieb (inkl. selbst verwaltetem PostgreSQL — Hetzner bietet kein
  DBaaS) und 4–8 h/Monat Betriebszeit; wirtschaftlich bei realistischer
  Zeitbewertung teurer als PaaS. Bleibt dokumentierter Migrationspfad
  (Container ist portabel).
- **Scaleway (Modell 3)** — *wartungsarme Nicht-PaaS-Alternative*:
  Managed PostgreSQL + TEM aus einer Hand; abgelehnt als Primärweg wegen
  fehlender nativer Review-Apps, UNGEKLÄRTER Managed-PG-Preise und
  cross-region gespeicherter DB-Backups (EU-intern, aber prüfpflichtig).
  Erste Ausweichoption, falls die Scalingo-Prüfung (H1–H5) scheitert.
- **OVHcloud:** einzige Kombination deutsche Vertragspartei (laut
  AGB-PDFs) + DE-Rechenzentrum + C5; zurückgestellt wegen schwächster
  Preistransparenz, 12-Monats-Anbieterlogs, Aiven Oy als
  Managed-DB-Subprozessor und EU-only-Support nur im Enterprise-Plan.
  Kandidat, falls später „maximale DE-Compliance" gefordert wird (B2B).
- **IONOS/STACKIT:** zurückgestellt (Preis-/Informationstransparenz im
  Self-Service zu gering für eine belastbare MVP-Entscheidung).
- **Clever Cloud:** valider Scalingo-Ersatz; Preisbeleglage (Stand 2023)
  zu unsicher.
- **Vercel:** nicht weiterverfolgt (US-Vertragspartei; EU-Datenresidenz
  über alle Dienste UNGEKLÄRT) — Priorisierung, keine Rechtsbewertung.
- **Kubernetes (Modell 4):** verworfen — überdimensioniert.

## Konsequenzen

### Positiv
- Ein Framework, ein Anbieter, ein AVV für den Kern; Review-Apps stärken
  den bereits beschlossenen PR-Workflow unmittelbar.
- Betriebsaufwand < 1 h/Monat im MVP; DB-Backups + PITR (Business-Plan)
  ohne Eigenbau; Zweitsicherung bei unabhängigem EU-Anbieter.
- Kostenrahmen klein und planbar (≈ 30–40 €/Monat MVP; ≈ 230–395 €/Monat
  bei 50.000 Registrierten — Korridore, `docs/cost-estimate.md`).
- Volle Portabilität: Node-Container + Standard-PostgreSQL + Dateien im
  Git — Anbieterwechsel bleibt realistisch (dokumentierter Pfad: Modell 1/3).

### Negativ / Risiken
- Kein deutscher Serverstandort (Frankreich/Outscale) — falls später ein
  DE-Standort gefordert wird (z. B. B2B-Kunden), steht der
  OVHcloud-/Hetzner-Pfad bereit; Wechselkosten moderat dank Portabilität.
- Scalingo ist ein kleinerer Anbieter; Abhängigkeit wird durch die
  tägliche externe Zweitsicherung und Container-Portabilität begrenzt.
- Astro-Governance liegt seit 01/2026 personell bei Cloudflare —
  beobachten; MIT-Lizenz + TSC + portable Inhalte begrenzen das Risiko;
  SvelteKit als dokumentierte Rückfalloption.
- Mehrere Preisangaben sind UNGEKLÄRT (H5) — die Kostenschätzung arbeitet
  mit Korridoren; Verifikation vor Vertragsschluss ist Freigabebedingung.

## Bestätigung durch den Auftraggeber (2026-07-15)

Der Auftraggeber hat ADR-0002 am 2026-07-15 mit folgenden Festlegungen
bestätigt:

### 1. Framework (bestätigt)
- Astro als primäres Web-Framework; Svelte-Islands für interaktive
  Lernkomponenten; Node-Adapter für dynamische, authentifizierte
  Funktionen.
- **Versionsregel:** Bei Implementierung wird die dann aktuelle **stabile**
  Version verwendet. Keine Beta-, RC- oder Preview-Versionen ohne
  separate Freigabe. Die konkrete Version wird reproduzierbar im
  Lockfile fixiert.

### 2. Hosting und Datenbank (als Zielarchitektur bestätigt)
- Scalingo (EU-PaaS), Scalingo Managed PostgreSQL, GitHub Actions für CI
  und Publikations-Gates, Review Apps für Pull Requests,
  Produktionsdeployment **nur nach manueller Freigabe** — es gibt keine
  automatische Produktion.
- **Diese Architekturentscheidung ist keine rechtliche,
  datenschutzrechtliche oder vertragliche Anbieterfreigabe.** Vor
  Vertragsschluss und Produktivdeployment sind mindestens zu prüfen und
  zu dokumentieren: vollständiger DPA/AVV, Subprozessorenliste, mögliche
  Nicht-EU-Datenzugriffe, Supportzugriffe, Log-Aufbewahrungsfristen,
  Backup-Speicherorte, Backup-Verschlüsselung, Lösch- und
  Exportmöglichkeiten, technische und organisatorische Maßnahmen (TOMs),
  aktuelle Preise und Vertragsbedingungen.

### 3. Zweitsicherung (bestätigt als geplant, nicht aktiviert)
- Hetzner Object Storage in deutscher bzw. geeigneter EU-Region ist
  **bevorzugter Kandidat** für die verschlüsselte Zweitsicherung.
- Aktivierung erst nach Prüfung von: AVV, Datenstandort, Verschlüsselung,
  Schlüsselverwaltung, Aufbewahrungsfrist, automatischer Löschung,
  Wiederherstellungstest, zusätzlicher Komplexität der
  Auftragsverarbeiterkette.
- Bis dahin: **geplante, aber nicht aktivierte Produktionsanforderung.**

### 4. Fallback-Reihenfolge (verbindlich dokumentiert)
1. **Scalingo** (Primärweg)
2. **Scaleway** (bevorzugte PaaS-/Managed-Service-Alternative)
3. **Hetzner VM** (kostenorientierter, wartungsintensiver Migrationspfad)

Ein Wechsel zu einer Alternative erfordert eine **neue oder aktualisierte
Architekturentscheidung** (ADR).

### 5. E-Mail-Anbieter (zurückgestellt)
- Scaleway Transactional Email bleibt bevorzugter Kandidat. Endgültige
  Auswahl erst nach Prüfung von AVV, Subprozessoren, Datenstandort,
  Logfristen, Zustellbarkeit und aktuellen Preisen. **Bis dahin: keine
  Integration, kein Vertragsschluss.**

### 6. H1–H7 als verpflichtende Produktivstart-Gates
- Die offenen Punkte H1–H7 (`docs/hosting-comparison.md` §5) sind
  **verpflichtende Produktivstart-Gates**.
- Vorläufig verantwortlich: **Legal/Regulatory Reviewer** und
  **Privacy/Security Reviewer** (Rollen gemäß
  `docs/security-and-privacy-rules.md` §5.3). Solange keine konkreten
  Personen benannt sind, dürfen die Gates **nicht als abgeschlossen
  markiert werden**.
- Die offenen Prüfungen blockieren **nicht**: Contentmodellierung,
  lokale Entwicklung, Entwicklung mit lokalen/synthetischen Daten,
  automatisierte Tests.
- Sie blockieren: Vertragsschluss mit den Anbietern, Verarbeitung realer
  Nutzerdaten, Produktivdeployment, öffentlichen Plattformstart.

## Freigabebedingungen (vor Umsetzung dieses ADR)

1. **H1–H7 aus `docs/hosting-comparison.md` abarbeiten** — insbesondere
   juristische Prüfung von Scalingo-DPA/Subprozessoren (H1),
   Supportzugriff (H2), Log-Fristen vs. §5.1 (H3), Live-Preise (H5),
   E-Mail-Anbieter (H7). **Dieses ADR simuliert keine dieser Prüfungen.**
2. Bestätigung des Auftraggebers zu Framework (Astro + Svelte-Islands),
   Anbieter (Scalingo) und Zweitsicherungs-Anbieter (Hetzner Object
   Storage) — einzeln widerspruchsfähig.
3. Kein Vertragsschluss, kein Account-Setup, keine Pipeline-Aktivierung
   vor dieser Freigabe.

## Folgeentscheidungen

| # | Gegenstand | Abhängigkeit |
|---|---|---|
| ADR-0003 | Content-Schemata (Lektion, Quiz, Simulation, Ampel, Prompt-Vorlage) | nach Freigabe ADR-0002 |
| ADR-0004 | Suchtechnik (Build-Index vs. Engine) | **nach** ADR-0003 (Vorgabe Auftraggeber) |
| — | E-Mail-Anbieter inkl. AVV (H7) | vor Implementierung der Registrierung |
| — | Zahlungsanbieter (Ausbaustufe 1) | nach MVP |
