# Initiales Threat Model — VersicherungsTech KI-Akademie (MVP)

**Status:** Entwurf · lebendes Dokument (Review vor Implementierungsstart
und vor Launch)
**Stand:** 2026-07-14
**Grundlagen:** `docs/data-flow-overview.md` (Komponenten, Vertrauensgrenzen
TB1–TB4), `docs/security-and-privacy-rules.md`,
`docs/architecture-recommendation.md`
**Methode:** STRIDE-orientierte Analyse je Vertrauensgrenze, ergänzt um
projektspezifische Risiken (Paywall, Content-Integrität, Prüfungslogik).
Dieses Dokument dient der **defensiven** Absicherung der Plattform.

---

## 1. Schutzziele und Kronjuwelen

| Asset | Schutzziel (prioritär) | Warum |
|---|---|---|
| Nutzerdaten (E-Mail, Passwort-Hash, Lernstand) | Vertraulichkeit, Integrität | Personenbezogen; Vertrauensversprechen (US-10.x) |
| Inhalte inkl. regulatorischer Aussagen | **Integrität** | Manipulierte Rechts-/Sicherheitsinhalte wären ein Reputations- und Haftungsschaden — Inhalte sind das Produkt |
| Prüfungs- und Zertifikatslogik | Integrität | Wertlosigkeit des Nachweises bei Manipulierbarkeit |
| Premium-Gating | Integrität | Geschäftsmodell |
| Verfügbarkeit der Plattform | Verfügbarkeit (nachrangig zum MVP-SLO) | NFR-F1: „werktags zuverlässig“, kein 24/7-Anspruch |
| Repository/CI (Quellcode + Inhalte) | Integrität, Zugriffsschutz | Supply-Chain zur Produktion (TB3/TB4) |

Entlastend wirkt die Architektur selbst: **kein** Zahlungsdatenbestand
(E2a), **keine** Gesundheits-/Kundendaten (nur synthetische Übungsdaten),
**kein** Personenbezug in Inhalten, minimales Nutzerdatenmodell.

## 2. Angreiferbilder

| Akteur | Motivation | Fähigkeiten |
|---|---|---|
| Anonymer Internet-Angreifer (TB1) | Opportunistisch: Credential Stuffing, Scraping, Defacement | Automatisierte Tools |
| Trittbrettfahrer | Premium-Inhalte ohne Abo, Zertifikat ohne Prüfung | Browser-Devtools, geteilte Accounts |
| Neugierige/böswillige registrierte Nutzer | Fremde Lernstände/Daten einsehen (IDOR) | Authentifizierte API-Zugriffe |
| Kompromittiertes Redaktions-/Entwicklerkonto (TB3/TB4) | Inhalts-/Code-Manipulation | Git-Zugriff, PR-Rechte |
| Kompromittierte Abhängigkeit (Supply Chain) | Code-Ausführung im Build/Frontend | npm-Ökosystem |
| Phishing gegen Lernende | Zugangsdaten, gefälschte Zertifikate | Gefälschte Mails/Seiten |

## 3. Bedrohungen und Gegenmaßnahmen (STRIDE je Grenze)

### TB1 — Browser ↔ Plattform (öffentlich)

| ID | Bedrohung (STRIDE) | Szenario | Gegenmaßnahmen (MVP-Pflicht) |
|---|---|---|---|
| T1 | Spoofing | Credential Stuffing / Brute Force auf Login | Passwort-Hashing nach Stand der Technik (z. B. Argon2id), Rate-Limiting auf Login/Registrierung/Reset, generische Fehlermeldungen, E-Mail-Verifizierung; Passwort-Mindestregeln ohne Schikane |
| T2 | Spoofing | Session-Diebstahl | HttpOnly-, Secure-, SameSite-Cookies; Session-Rotation nach Login; serverseitige Session-Invalidierung bei Logout/Passwortwechsel |
| T3 | Tampering | Manipulierte Fortschritts-/Prüfungs-Requests („Modul als abgeschlossen melden“, Prüfungsantworten fälschen) | Alle Bewertungs- und Zulassungslogik **serverseitig** (AC-13); Client meldet nur Ereignisse; Plausibilitätsprüfung (z. B. Prüfung nur bei erfüllter Zulassung, serverseitig gezogene Fragen aus dem Pool) |
| T4 | Tampering | XSS über Eingabefelder (Anzeigename, Freitext-Feedback M-E2) | Konsequentes Output-Encoding, CSP ohne unsafe-inline, Eingabelängen-Limits; Freitexte nie als HTML rendern |
| T5 | Information Disclosure | **Paywall-Umgehung:** Premium-Inhalte im öffentlichen Bundle/Suchindex | Premium-Volltexte nur nach serverseitiger Berechtigungsprüfung ausliefern; öffentlicher Suchindex enthält von Premium-Inhalten nur Titel/Snippet (AC-17/FR-15.4); Test: unautorisierter Direktabruf aller Premium-URLs schlägt fehl |
| T6 | Information Disclosure | IDOR: fremden Lernstand/fremdes Zertifikat abrufen | Autorisierung auf jeder Ressource (Konto-Scope), keine erratbaren IDs für Zertifikats-Verifikationscodes (lange Zufalls-Codes), automatisierte Zugriffstests |
| T7 | Information Disclosure | Nutzer-Enumeration über Registrierungs-/Reset-Antworten | Einheitliche Antworten und Timing unabhängig von Kontoexistenz |
| T8 | Elevation of Privilege | Zugriff auf Admin-Funktionen (Premium-Flag setzen) | Getrennte Admin-Rolle, Zwei-Faktor-Authentisierung für Admin/Redaktion, Audit-Log für Premium-Flag-Änderungen |
| T9 | DoS | Lastspitzen/einfache Flood-Angriffe | Statische Auslieferung + Caching (inhärent robust), Rate-Limits auf Schreibpfaden; im MVP genügt Basis-Schutz des Hosters (NFR-F1) |
| T10 | Repudiation | Streit über Prüfungsergebnis/Zertifikatsausstellung | Zeitstempel + Versuchshistorie serverseitig; Zertifikatsdatensatz mit Kursversion |

### TB2 — Plattform ↔ E-Mail-Dienst

| ID | Bedrohung | Szenario | Gegenmaßnahmen |
|---|---|---|---|
| T11 | Spoofing | Phishing-Mails im Namen der Akademie | SPF/DKIM/DMARC korrekt konfiguriert; Mails ohne Login-Links-Wildwuchs (nur Verifizierung/Reset); einheitlicher Absender |
| T12 | Information Disclosure | E-Mail-Dienst als Datenabfluss | EU-Anbieter mit AV-Vertrag (DF4); nur E-Mail-Adresse und Vorgangstyp übertragen, keine Lernstands- oder Prüfungsdaten in Mails |
| T13 | Tampering | Reset-Link-Missbrauch | Einmal-Tokens mit kurzer Gültigkeit, Invalidierung nach Nutzung, kein Konto-Hinweis in Fehlerfällen |

### TB3/TB4 — Redaktion, Repository, CI/CD, Deployment

| ID | Bedrohung | Szenario | Gegenmaßnahmen |
|---|---|---|---|
| T14 | Tampering | **Inhaltsmanipulation:** kompromittiertes Konto ändert regulatorische Inhalte oder entfernt Sicherheitshinweise | Branch-Protection (kein Direkt-Push auf Hauptbranch), Pflicht-Review durch zweite Person, erzwungene CI-Gates (Regulatorik-Marker-Logik), 2FA für alle Git-Konten, Audit über PR-Historie (AC-16.5) |
| T15 | Tampering | Umgehung der Publikations-Gates („Regulatorik-Review überspringen“) | Gates laufen in CI als Pflicht-Checks, nicht als Konvention; Status-Regeln maschinell geprüft (AC-16.3); Vier-Augen-Merge |
| T16 | Tampering | Supply-Chain: bösartige/kompromittierte Abhängigkeit | Lockfiles, Dependency-Review/Updates als Prozess, minimale Abhängigkeiten, automatisierte Schwachstellen-Scans im CI |
| T17 | Information Disclosure | Secret gelangt ins Repository | Regel „keine Secrets im Repo“ + automatischer Secret-Scan im CI (AC-20.3); Secrets nur als Umgebungsvariablen/Deployment-Secrets; Rotationsprozess bei Vorfall (`docs/security-and-privacy-rules.md` §2) |
| T18 | Elevation of Privilege | Unbefugtes Deployment in Produktion | Deployment nur nach ausdrücklicher Freigabe (technisch: geschützte Deployment-Umgebung mit Freigabe-Schritt); getrennte Zugänge für Staging/Produktion |
| T19 | Repudiation | „Wer hat diesen Inhalt freigegeben?“ | PR-basierte Review-Dokumentation (Person, Datum, Kommentar) — nativer Bestandteil des Git-Workflows |

### Datenbank und Betrieb

| ID | Bedrohung | Szenario | Gegenmaßnahmen |
|---|---|---|---|
| T20 | Information Disclosure | DB-Kompromittierung | Minimal-Datenmodell (Schadensbegrenzung by Design), Verschlüsselung at rest, DB nicht öffentlich erreichbar (privates Netz), restriktive DB-Rechte der App |
| T21 | Information Disclosure | Backup-Abfluss | Verschlüsselte Backups, EU-Speicherort, Zugriff auf Betriebsrollen beschränkt (DF3) |
| T22 | Tampering/Repudiation | Unbemerkte Datenänderung durch Betrieb/Admin | Audit-Log für Admin-Aktionen (mind. Premium-Flag, Kontolöschung); so wenige Admin-Konten wie möglich |
| T23 | Information Disclosure | Logs enthalten mehr als nötig | Log-Richtlinie: keine Passwörter/Tokens/Antwortinhalte in Logs; kurze Aufbewahrung (DF2) |

## 4. Projektspezifische Missbrauchsfälle

| ID | Fall | Bewertung | Behandlung |
|---|---|---|---|
| M1 | Zertifikatsfälschung (PDF nachgebaut) | PDF allein ist fälschbar — bekannt und akzeptiert | Verifikationsseite (E7) als Echtheitsanker; Zertifikat verweist auf Verifikationscode |
| M2 | Account-Sharing (ein Premium-Konto, viele Nutzer) | Umsatzrisiko, kein Sicherheitsrisiko | Im MVP akzeptiert; beobachten; keine invasive Gerätekontrolle (widerspräche Datensparsamkeit) — ENTSCHEIDUNG AUFTRAGGEBER bei Ausbaustufe |
| M3 | Prüfungs-Antworten öffentlich geteilt | Entwertung der Prüfung | Fragenpool mit Variation (FR-11.5); Korridor-Monitoring der Bestehensquote (`docs/success-metrics.md` 3.3) |
| M4 | Scraping der freien Inhalte | Gering — freie Inhalte sind bewusst öffentlich | Kein Schutz nötig; Premium-Inhalte durch T5-Maßnahmen geschützt |
| M5 | Missbrauch des Freitext-Feedbacks (M-E2) für Spam/Schadinhalte | Gering | Längenlimit, kein öffentliches Rendern, Rate-Limit |

## 5. Bewusst außerhalb des Scopes (MVP)

- Kein Schutzbedarf für Zahlungsdaten (keine Bezahlstrecke — E2a).
- Kein Mandanten-/B2B-Zugriffsmodell (existiert nicht im MVP).
- Kein LLM-Prompt-Injection-Risiko in der Plattform (keine Live-LLM-Anbindung
  — E4); **bei Ausbaustufe 2 ist dieses Threat Model zu erweitern**
  (Prompt Injection, Datenabfluss an KI-APIs, Kostenmissbrauch).
- Hochverfügbarkeits-/DDoS-Szenarien über Basis-Schutz hinaus (NFR-F1).

## 6. Prüf- und Pflegeplan

1. **Vor Implementierungsstart:** Review dieses Dokuments gegen die
   finalen ADRs (0002 ff.); Maßnahmen T1–T23 in die technischen Tickets
   übernehmen.
2. **Vor Launch:** Verifikation der Pflicht-Maßnahmen (Checkliste aus
   Spalte „Gegenmaßnahmen“), automatisierter Dependency- und Secret-Scan
   grün, Negativtests aus AC-16/17/20 bestanden; leichte manuelle
   Sicherheitsprüfung der Kernflüsse (Login, IDOR, Paywall).
3. **Laufend:** Threat Model bei jeder Architekturänderung (neues ADR)
   aktualisieren; spätestens bei Ausbaustufe 1 (Bezahlstrecke) und 2
   (Live-LLM) verpflichtende Erweiterung.
