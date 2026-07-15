# Framework-Vergleich — VersicherungsTech KI-Akademie (MVP)

**Status:** Entwurf zur Entscheidung (Teil der ADR-0002-Unterlagen)
**Stand:** 2026-07-15 · Abrufdatum aller Quellen: **2026-07-15**
**Grundlagen:** ADR-0001 (Accepted), `docs/product-requirements.md`,
`docs/architecture-recommendation.md`

**Methodik und Beleglage:** Alle Framework-Fakten stammen aus offiziellen
Quellen (Projekt-Dokumentation, offizielle Blogs, npm-Registry als
offizieller Distributionskanal). Direkte Seitenabrufe waren in der
Rechercheumgebung teilweise durch einen Netzwerk-Proxy blockiert; in diesen
Fällen wurden domainbeschränkte Suchauszüge der offiziellen Seiten
verwendet. Solche Angaben sind vor endgültiger Festlegung gegen die
Live-Dokumentation zu verifizieren; nicht offiziell Belegbares ist als
**UNGEKLÄRT** markiert.

---

## 1. Kandidaten und Grunddaten

| | Next.js | Astro | SvelteKit | Nuxt |
|---|---|---|---|---|
| Stabile Version (npm `latest`) | 16.2.10 (01.07.2026) | 7.0.9 (13.07.2026) | 2.69.3 (13.07.2026); v3 in Pre-Release | 4.4.8 (08.06.2026) |
| Lizenz | MIT | MIT | MIT | MIT |
| Governance | Vercel Inc. (Firmenprojekt) | Offene Governance mit Technical Steering Committee; Kernteam seit 01/2026 bei Cloudflare angestellt | Unabhängiges OSS-Projekt; Vercel beschäftigt Kern-Maintainer; „Governance does not change" (offizielle Aussage) | NuxtLabs, seit 07/2025 Teil von Vercel; laut Ankündigung weiterhin offene Governance |
| UI-Modell | React (Server + Client Components) | Islands: offiziell React, Preact, Svelte, Vue, SolidJS, Alpine | Svelte 5 (Compiler) | Vue 3 |

Quellen (Abruf 2026-07-15): registry.npmjs.org/next, /astro,
/@sveltejs/kit, /nuxt; nextjs.org/blog/next-16;
astro.build/blog/astro-7/; astro.build/blog/joining-cloudflare/;
svelte.dev/blog/accelerating-sveltes-development;
vercel.com/blog/nuxtlabs-joins-vercel; github.com/sveltejs/kit/releases.

Als „weitere begründete Alternative" wurde **Nuxt** aufgenommen (viertes
großes Meta-Framework mit offiziellem Content-Modul — der naheliegendste
zusätzliche Kandidat für eine inhaltsgetriebene Plattform). Bewusst nicht
aufgenommen: reine Static-Site-Generatoren (Eleventy, Hugo — keine
integrierte App-Schicht für Auth/Fortschritt) und reine SPA-Frameworks
(kein statisches Content-Rendering).

## 2. Bewertung entlang der projektkritischen Kriterien

### 2.1 Markdown/MDX und Content-Validierung (Kernanforderung aus ADR-0001)

| Framework | Befund | Quelle (Abruf 2026-07-15) |
|---|---|---|
| **Astro** | Markdown nativ; **offizielle MDX-Integration** (`@astrojs/mdx`). **Content Collections mit Zod-Schema-Validierung**: Frontmatter/Einträge werden gegen definierte Schemata validiert, mit automatischen TypeScript-Typen; Content-Loader-API für eigene Quellen (z. B. YAML-Übungsdefinitionen) | docs.astro.build/en/guides/integrations-guide/mdx/; docs.astro.build/en/guides/content-collections/ |
| Next.js | Offizielle `@next/mdx`-Integration; **keine eingebaute Schema-Validierung** für Frontmatter/Content gefunden (UNGEKLÄRT/Eigenbau, z. B. mit Zod + Velite/Contentlayer-Nachfolgern — Drittprojekte) | nextjs.org/docs/app/guides/mdx |
| SvelteKit | **Keine offizielle MDX-Unterstützung**; Community-Paket `mdsvex` ist als offizielles CLI-Add-on dokumentiert; Schema-Validierung: Eigenbau | svelte.dev/docs/cli/mdsvex; svelte.dev/docs/kit/integrations |
| Nuxt | Kein MDX; offizielles Modul `@nuxt/content` mit MDC-Syntax (Vue-Komponenten in Markdown); Collections mit Schema laut Doku vorhanden, Details UNGEKLÄRT | content.nuxt.com/docs/files/markdown; nuxt.com/modules/content |

**Einordnung:** ADR-0001 verlangt schemavalidierte deklarative Inhalte mit
Build-Gates. Astro liefert genau diesen Mechanismus als stabiles
Kern-Feature; bei allen anderen ist er Eigenbau oder Drittabhängigkeit.
Dies ist das gewichtigste Einzelkriterium des Vergleichs.

### 2.2 Statisch + dynamisch in einem Projekt

Alle vier beherrschen Hybrid-Rendering stabil; Unterschiede liegen im Modell:

- **Astro:** Standard = Prerendering; einzelne Routen/Endpoints mit
  `prerender = false` serverseitig („On-demand Rendering", Adapter nötig);
  zusätzlich Server Islands für dynamische Komponenten in statischen Seiten
  (docs.astro.build/en/guides/on-demand-rendering/, /server-islands/).
  Passt exakt zum Zuschnitt „statische Inhalte + kleine App-Schicht".
- **SvelteKit:** `prerender`-Page-Option pro Seite/Layout; API-Routen als
  `+server.js` (svelte.dev/docs/kit/page-options).
- **Next.js:** Static/Dynamic Rendering pro Route, Route Handlers;
  Partial Prerendering/„Cache Components": Stabilitätsstatus in 16.2
  UNGEKLÄRT (nextjs.org/docs/app/building-your-application/rendering/…).
- **Nuxt:** Route Rules (`prerender`, `swr`, `isr` je Route), Nitro-API-
  Routen; Hybrid nicht mit `nuxt generate` kombinierbar
  (nuxt.com/docs/4.x/guide/concepts/rendering).

### 2.3 Self-Hosting und Portabilität (EU-Hosting-Pflicht)

| Framework | Befund |
|---|---|
| Astro | Offizieller Node-Adapter (`@astrojs/node`, Standalone/Middleware); unterstützt Server Islands, Actions, Sessions; keine plattformexklusiven Kern-Features gefunden (docs.astro.build/en/guides/integrations-guide/node/) |
| SvelteKit | Offizieller `adapter-node` (Standalone-Server, Precompression eingebaut); keine Vercel-exklusiven Features gefunden (svelte.dev/docs/kit/adapter-node) |
| Nuxt | Nitro `node_server`-Preset ist Build-Standard; eigenständiger Node-Server (nuxt.com/docs/4.x/getting-started/deployment) |
| Next.js | `next start`/`output: 'standalone'` offiziell; **dokumentierte Self-Hosting-Caveats:** ISR-/Cache-Propagation bei Multi-Instanz nur mit eigenem `cacheHandler`, `sharp` für Bildoptimierung (nextjs.org/docs/app/guides/self-hosting) |

Alle vier laufen als Container auf jedem EU-Hoster. Next.js trägt die
meiste plattformnahe Komplexität ins Self-Hosting; die „Vercel-Gravitation"
ist dokumentierbar real, wenn auch beherrschbar.

### 2.4 Interaktive Lernkomponenten (Quiz, Simulation, Datenampel, Prompt-Bausatz)

- **Astro:** Islands-Architektur — interaktive Übungen als gezielt
  hydratisierte Komponenten in ansonsten statischen Lektionsseiten; freie
  Wahl des Komponenten-Frameworks (offiziell u. a. Svelte, React, Preact,
  Vue). Minimale JS-Auslieferung auf reinen Leseseiten (NFR-B/C).
- **SvelteKit/Next.js/Nuxt:** Voll geeignet; liefern aber
  framework-typisch mehr Laufzeit-JS auf Inhaltsseiten aus (bei Next.js/
  Nuxt durch RSC/Lazy Hydration gemildert).

### 2.5 Authentifizierung und Sessions (FR-16, SSO-Ausbaustufe)

Kein Kandidat bringt ein vollständiges Auth-System mit — das ist für unser
Minimal-Datenmodell akzeptabel (bewusste Eigenimplementierung hinter
schmaler Schnittstelle, siehe ADR-0001/Threat Model T1–T2):

- Astro: **Sessions-API stabil** (seit 5.7); offizieller Auth-Guide nennt
  Auth.js, Better Auth, Lucia (docs.astro.build/en/guides/sessions/).
- SvelteKit: `event.locals`-Muster; Lucia und Better Auth als offizielle
  CLI-Add-ons dokumentiert (svelte.dev/docs/kit/auth).
- Next.js: offizieller Guide empfiehlt iron-session / Auth.js
  (nextjs.org/docs/app/guides/authentication).
- Nuxt: offizielles Rezept mit `nuxt-auth-utils`
  (nuxt.com/docs/4.x/guide/recipes/sessions-and-authentication).

SSO/OIDC ist in allen vier Fällen über dieselben Bibliotheken
(Auth.js/Better Auth) nachrüstbar — kein Differenzierungskriterium.

### 2.6 Barrierefreiheit (AC-18)

- **SvelteKit:** stärkste eingebaute Unterstützung — Compiler-a11y-
  Warnungen zur Entwicklungszeit + Live-Region-Ansagen und Fokus-Management
  bei Client-Navigation (svelte.dev/docs/svelte/compiler-warnings,
  /docs/kit/accessibility).
- **Astro:** Dev-Toolbar-Audit prüft a11y-Muster im Dev-Modus; kein
  eingebauter Route Announcer (Verhalten mit View Transitions UNGEKLÄRT) —
  bei überwiegend statischen Volltext-Navigationen (MPA-Modell) ist das
  strukturell weniger kritisch, da der Browser selbst die Navigation
  handhabt.
- **Next.js:** Route Announcer + `eslint-plugin-jsx-a11y` in
  Standard-Konfiguration.
- **Nuxt:** `<NuxtRouteAnnouncer>`/`<NuxtAnnouncer>`.

In allen Fällen bleibt die a11y-Qualität der Übungskomponenten
Eigenverantwortung (AC-18-Tests). Kombination Astro + **Svelte-Islands**
holt die Svelte-Compiler-Warnungen in die Übungskomponenten.

### 2.7 Mehrsprachigkeit (technisch vorbereiten, MVP Deutsch)

- Astro: **eingebautes i18n-Routing** (Locales, Fallbacks, Helper) —
  docs.astro.build/en/guides/internationalization/.
- Nuxt: offizielles `@nuxtjs/i18n`-Modul.
- Next.js (App Router): kein eingebautes i18n; Locale-Segment + Middleware
  + Drittbibliothek (offizieller Guide).
- SvelteKit: kein Kern-i18n; Paraglide als offizielles CLI-Add-on.

### 2.8 Suche, Lernfortschritt, PostgreSQL, Preview-Deployments

- **Suche:** In allen vier Fällen Build-Index oder externe Engine —
  framework-neutral; Entscheidung fällt in ADR-0004 nach den
  Content-Schemata (Vorgabe des Auftraggebers).
- **Lernfortschritt/PostgreSQL:** App-Schicht mit Node.js-Postgres-Client
  bzw. leichtgewichtigem ORM — in allen vier Frameworks gleichwertig
  umsetzbar; kein Differenzierungskriterium.
- **Preview-Deployments:** Eigenschaft des Hostings (siehe
  `docs/hosting-comparison.md`), nicht des Frameworks; alle vier bauen in
  CI zu einem Container/Node-Artefakt.

### 2.9 Git-Review-Workflow und spätere Git-basierte Editor-UI

Alle vier arbeiten mit Dateien im Repository. Astros Content Collections
machen die PR-Prüfung am stärksten: Schema-Fehler (fehlender Rechtsstand,
fehlende Quellen, unbekannte Felder) brechen den Build maschinell — genau
die geforderten Gates (NFR-E4, AC-15/16). Git-basierte Editor-UIs
(z. B. Sveltia/Decap) arbeiten formatneutral auf Markdown/YAML und sind mit
allen vier kompatibel.

### 2.10 Vendor Lock-in und Projektrisiko

| Framework | Einschätzung |
|---|---|
| Astro | MIT, offene Governance (TSC); Kernteam seit 01/2026 bei Cloudflare — Risiko einer Cloudflare-Priorisierung ist zu beobachten, bisher keine plattformexklusiven Kern-Features; Inhalte (MD/MDX/YAML) und Islands-Komponenten sind portabel |
| SvelteKit | Unabhängigstes Projekt; kleinster Firmen-Einfluss auf Roadmap |
| Next.js | Stärkste Kopplung an einen Anbieter (Vercel führt das Projekt); Self-Hosting-Caveats dokumentiert |
| Nuxt | NuxtLabs bei Vercel; laut Ankündigung offene Governance, Konstellation aber jung |

## 3. Zusammenfassende Matrix

Skala: ++ / + / o / − (bezogen auf **dieses** Projekt).

| Kriterium | Next.js | **Astro** | SvelteKit | Nuxt |
|---|:---:|:---:|:---:|:---:|
| Markdown/MDX offiziell | + | ++ | o | o (MDC statt MDX) |
| Content-Schema-Validierung eingebaut | − | ++ | − | + (Details UNGEKLÄRT) |
| Statisch+dynamisch hybrid | + | ++ | ++ | + |
| Self-Hosting/Portabilität | o | ++ | ++ | + |
| Interaktive Übungs-Inseln / wenig JS auf Leseseiten | o | ++ | + | o |
| Auth/Sessions-Grundlage | + | + | + | + |
| Barrierefreiheit eingebaut | + | o/+ | ++ | + |
| i18n vorbereitet | o | ++ | o | + |
| Lock-in-/Governance-Risiko | − | o/+ | ++ | o |
| Eignung Git-Gates (Build-Validierung) | o | ++ | o | + |

## 4. Ergebnis

**Empfehlung: Astro** (mit `@astrojs/node`-Adapter für das EU-Self-Hosting
und **Svelte als Island-Framework** für die interaktiven Übungskomponenten,
um deren Compiler-a11y-Warnungen zu nutzen — Alternative Preact/React ohne
Architekturfolgen).

Begründung in einem Satz: Astro ist das einzige Framework, das die
Kernanforderung aus ADR-0001 — schemavalidierte, deklarative Inhalte mit
Build-Gates — als stabiles Kern-Feature mitbringt, und sein Islands-Modell
liefert die leichtesten, am besten kontrollierbaren Lektionsseiten für
eine textbasierte, mobile Lernplattform.

**Zweitplatzierter:** SvelteKit — beste eingebaute Barrierefreiheit und
unabhängigste Governance, aber Content-Tooling (MDX-Äquivalent,
Schema-Validierung) wäre Eigenbau; sinnvoller Rückfallweg, falls sich die
Astro/Cloudflare-Konstellation negativ entwickelt (Inhalte blieben
weitgehend portabel).

Formale Entscheidung: `docs/adr/0002-framework-hosting.md`
(Status: Accepted, 2026-07-15 — mit Versionsregel: nur stabile Releases,
im Lockfile fixiert; keine Beta-/RC-/Preview-Versionen ohne separate
Freigabe).
