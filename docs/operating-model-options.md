# Betriebsmodell-Optionen — VersicherungsTech KI-Akademie (MVP)

**Status:** Entwurf zur Entscheidung (Teil der ADR-0002-Unterlagen)
**Stand:** 2026-07-15
**Grundlagen:** ADR-0001 (Accepted), `docs/architecture-recommendation.md`,
`docs/threat-model-initial.md`, `docs/data-flow-overview.md`
**Anbieter-Fakten und Preise:** `docs/hosting-comparison.md` ·
**Kosten:** `docs/cost-estimate.md`

Dieses Dokument vergleicht die vier Betriebsansätze unabhängig vom
konkreten Anbieter: Wer trägt welche Betriebsverantwortung, und was
bedeutet das für ein kleines Team ohne dedizierten Betriebsingenieur?

---

## 1. Was betrieben werden muss (aus ADR-0001)

| Baustein | Charakter |
|---|---|
| Statisch generierte Inhalte + Suchindex | Build-Artefakt; anspruchslos (Dateien ausliefern) |
| App-Server (Node.js): Auth, Fortschritt, Prüfung, Zertifikat | Dauerhaft laufender Prozess; sicherheitskritisch (Threat Model T1–T10) |
| PostgreSQL (Minimal-Nutzerdatenmodell) | Zustandsbehaftet; Backups Pflicht (≤ 30 Tage, §5.1 Sicherheitsregeln) |
| Transaktions-E-Mail | Externer Dienst in jedem Modell (TB2) |
| CI/CD mit Publikations-Gates | Läuft beim Git-Hoster; unabhängig vom Hosting-Modell |
| Preview-Deployments für PR-Review | Je nach Modell eingebaut oder selbst zu bauen |
| Monitoring/Alarme, TLS, DNS | In jedem Modell nötig, unterschiedlich viel Eigenleistung |

Die Last ist niedrig und lesedominiert (Textplattform, statische Inhalte,
kleine Schreibzugriffe für Fortschritt) — **jedes** der vier Modelle trägt
die Zielgrößen bis 50.000 registrierte Nutzer technisch problemlos. Die
Entscheidung fällt über Betriebsverantwortung, Datenschutz-Papierlage und
Kosten, nicht über Skalierung.

## 2. Die vier Modelle

### Modell 1 — Selbst gehostete Anwendung auf VM(s) in EU-Region

App + PostgreSQL + Reverse Proxy auf ein bis zwei virtuellen Maschinen
(z. B. bei einem deutschen Anbieter), Deployment per Container und
CI-Pipeline; optional eine Self-Hosting-PaaS-Schicht (z. B. Coolify) für
Komfortfunktionen.

| Aspekt | Bewertung |
|---|---|
| Eigenverantwortung | **Maximal:** OS-Patches, Docker-Updates, Postgres-Betrieb inkl. Backups + Restore-Tests, TLS, Härtung, Monitoring, Incident-Bereitschaft |
| Datenschutz-Papierlage | Einfachste Kette: ein AVV mit dem VM-Anbieter (+ E-Mail-Dienst); volle Kontrolle über Logs/Backups |
| Preview-Deployments | Selbst zu bauen (CI-Job + Wildcard-Subdomains) oder via Coolify-PR-Deployments |
| Kosten | Niedrigste Infrastrukturkosten, höchste Personalkosten (Zeit) |
| Risiko | Betriebsfehler des Teams (verpasste Patches, ungetestete Backups) ist das realistische Hauptrisiko — vgl. T16/T20/T21 |

**Passt, wenn:** Betriebs-Know-how und Bereitschaftszeit vorhanden sind und
Kostenminimierung Vorrang hat.

### Modell 2 — Europäischer Platform-as-a-Service-Anbieter (PaaS)

App und Managed PostgreSQL als Plattformdienste eines EU-PaaS
(z. B. Scalingo, Clever Cloud): Git-Push/GitHub-Integration, Plattform
übernimmt OS, Laufzeitumgebung, DB-Betrieb, Backups, Basis-Monitoring;
Review-Apps pro Pull Request teils eingebaut.

| Aspekt | Bewertung |
|---|---|
| Eigenverantwortung | **Minimal:** nur Anwendungscode und Konfiguration; kein OS-/DB-Patching |
| Datenschutz-Papierlage | Ein AVV mit dem PaaS; dessen Subprozessoren (Infrastruktur-Unterbau!) müssen geprüft werden — siehe `hosting-comparison.md` |
| Preview-Deployments | Bei geeigneten Anbietern eingebaut (Review Apps) — direkter Gewinn für den Git-Review-Workflow (E5) |
| Kosten | Höchster Preis pro Ressource; bei dieser kleinen Last absolut trotzdem moderat |
| Risiko | Anbieterbindung an Plattform-Konventionen (mittel — Container/Buildpacks bleiben portabel); Preisänderungen |

**Passt, wenn:** Das Team klein ist und Entwicklungszeit die knappste
Ressource — Betriebsaufwand wird eingekauft.

### Modell 3 — Europäischer Cloud-Anbieter mit Managed PostgreSQL

Mittelweg: App selbst betreiben (kleine VM oder Serverless-Container),
aber die **Datenbank als Managed-Dienst** (automatische Backups, Updates,
Failover-Optionen) beim selben EU-Cloud-Anbieter (z. B. Scaleway,
OVHcloud, IONOS, STACKIT).

| Aspekt | Bewertung |
|---|---|
| Eigenverantwortung | Mittel: App-Umgebung ja, aber die kritischste Betriebsaufgabe (DB-Backups/Restore/Patching) ist ausgelagert |
| Datenschutz-Papierlage | Ein AVV mit dem Cloud-Anbieter; ein Haus für App + DB + Object Storage |
| Preview-Deployments | Selbst zu bauen (wie Modell 1) oder über Serverless-Container-Varianten vereinfacht |
| Kosten | Zwischen Modell 1 und 2; Managed-DB kostet spürbar mehr als Self-Hosted-Postgres, kauft aber genau das größte Risiko weg |
| Risiko | Zwei Betriebswelten (eigene App-Umgebung + Cloud-Dienste) — etwas mehr Komplexität als Modell 2 |

**Passt, wenn:** Man Kontrolle über die App-Umgebung behalten will, aber
das Datenbank-Risiko (T20/T21, Backup-Pflichten) nicht selbst tragen möchte.

### Modell 4 — VM-/Containerbetrieb mit Orchestrierung

Containerplattform (Managed Kubernetes o. ä.) beim EU-Anbieter; App und
ggf. DB als Container-Workloads.

| Aspekt | Bewertung |
|---|---|
| Eigenverantwortung | Hoch: Cluster-Konzepte, Ingress, Zertifikate, Upgrades — zusätzlich zur App |
| Datenschutz-Papierlage | Wie Modell 3 |
| Preview-Deployments | Gut machbar (Namespaces pro PR), aber Eigenbau |
| Kosten | Grundkosten des Clusters übersteigen den Bedarf; kleinste sinnvolle Setups sind teurer als Modell 1–3 |
| Risiko | **Überdimensionierung:** Kubernetes löst Probleme (viele Services, viele Teams, Autoscaling-Druck), die dieses Projekt nicht hat |

**Passt, wenn:** Es eine bestehende Kubernetes-Betriebsorganisation gäbe —
die gibt es hier nicht. **Für den MVP nicht empfohlen.**

## 3. Gegenüberstellung

| Kriterium | M1 VM self-hosted | M2 EU-PaaS | M3 Cloud + Managed PG | M4 Kubernetes |
|---|:---:|:---:|:---:|:---:|
| Wartungsaufwand (Team-Zeit) | −− | ++ | o | −− |
| Infrastrukturkosten | ++ | o | + | − |
| Backup/Restore ohne Eigenleistung | − | ++ | ++ (DB) / o (App) | − |
| Preview-Deployments eingebaut | − (Eigenbau/Coolify) | ++ (anbieterabhängig) | − | − |
| Monitoring eingebaut | − | + | + | o |
| Portabilität (Container bleibt Container) | ++ | + | + | + |
| AVV-/Subprozessor-Kette einfach | ++ | o (Unterbau prüfen!) | + | + |
| Angemessenheit für Projektgröße | + | ++ | + | −− |

## 4. Einordnung für die Empfehlung

- **Modell 2 (EU-PaaS)** ist für dieses Projekt der beste Standardweg:
  kleines Team, sicherheitskritische, aber kleine App, Pflicht zu Backups
  und Review-Prozessen — genau die Dinge, die eine PaaS mitbringt.
  Voraussetzung: Die Subprozessor-/Datenstandort-Prüfung des konkreten
  Anbieters fällt positiv aus (siehe `hosting-comparison.md`, offene
  Punkte).
- **Modell 3** ist der robuste zweite Platz und der natürliche
  Ausweichpfad, falls die PaaS-Prüfung scheitert oder Preise sich ändern.
- **Modell 1** bleibt die kostengünstigste vertretbare Alternative —
  akzeptabel nur mit ehrlich eingeplanter Betriebszeit und getesteten
  Restore-Prozeduren.
- **Modell 4** wird verworfen (Überdimensionierung).

Die konkrete Anbieterwahl und die Gesamtempfehlung stehen in
`docs/adr/0002-framework-hosting.md` (Status: Accepted — Architektur
technisch akzeptiert; Anbieter rechtlich noch nicht freigegeben,
H1–H7 sind Produktivstart-Gates).
