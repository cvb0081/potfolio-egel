# egelxh.dev — Portfolio Projects Update (Design)

**Date:** 2026-06-15
**Status:** Approved
**Source spec:** egelxh.dev Portfolio Update Spec (June 15, 2026)

## Goal

Add 2 new project case studies, change one Key Metric, reorder projects, add
uniform highlight bullets to every project card, and refine the section subtitle.

## Scope

Two files only:

- `src/components/MetricsBar.astro`
- `src/components/Projects.astro`

No new components — both are data-driven (array → template map). No changes to
any other section, SEO, or design tokens.

## Decisions (confirmed with user)

1. **Selling points** → add a `highlights` bullet list to **all 6** cards (backfill
   the existing 4 so the format stays uniform).
2. **Display order** → recommended reorder: FlotaIme, Clinic, Hospitality, Tenant,
   Monitoring, SSO.
3. **Subtitle** → update to "Real systems I've built, led, and shipped. Business
   results paired with technical depth."

## Change 1 — MetricsBar

`{ value: '4', label: 'Products Shipped' }` → `{ value: 'Multiple', label: 'Products Shipped' }`.
Center-aligned in a 3-col grid; wider text is fine. Verify no mobile break.

## Change 2 — Projects data array

Final order and content:

1. **FlotaIme** (unchanged content) + highlights
2. **Healthcare Clinic Management Platform** (new)
3. **Hospitality Management Platform** (unchanged content) + highlights
4. **Tenant Management Platform** (new)
5. **Custom Monitoring & Alerting Platform** (unchanged content) + highlights
6. **Enterprise Single Sign-On Platform** (unchanged content) + highlights

Each project object gains `highlights: string[]` (3-4 concise, business-first items).

### New — Tenant Management Platform
- role: `Team Leader`
- metric: `{ value: '~3-4 Weeks', label: 'From zero to working MVP' }`
- summary + tech tags: from spec §3
- highlights: repeat-client trust · production observability from day one ·
  contract-first typed API (NSwag) · companion native iOS app

### New — Healthcare Clinic Management Platform
- role: `Team Leader & Lead Architect`
- metric: `{ value: 'Demo-Ready', label: 'In 8 weeks from takeover' }`
- summary + tech tags: from spec §4
- highlights: process transformation (267 raw commits → 187 PR-gated reviews) ·
  modular monolith, 4 bounded contexts, schema-per-module multi-tenancy ·
  architecturally enforced double-booking protection · ~700 tests (Testcontainers + Playwright E2E)

### Highlights for existing 4
- **FlotaIme:** sole owner of technical vision/architecture · multi-tenant + Clean
  Architecture from day one · onboarding pilot clients
- **Hospitality:** intelligent allocation engine resolves channel conflicts ·
  database-per-tenant across 50+ clients · payment fiscalization for compliance
- **Monitoring:** high-volume telemetry with time-series storage · configurable
  alerting + live dashboards · built from scratch, national scale
- **SSO:** federated identity across 4 products · zero-disruption ~35K-user
  migration · custom hash extensions rehash legacy creds on first login

## Change 3 — Card template

Add a highlights block between the summary `<p>` and the tech-stack div. Small muted
bullet list matching the card aesthetic (accent-teal marker, `text-sm`,
`text-text-secondary`). Rendered for every card.

Guard the right-aligned metric value (`shrink-0`) against ugly wrapping for the longer
new values (`~3-4 Weeks`, `Demo-Ready`) — verify render; add `whitespace-nowrap` or a
width guard only if needed.

## Change 4 — Subtitle

Update the Projects section subtitle string per decision 3.

## Content style

Business-first, simple, concise, anonymized (only FlotaIme named). Tech tags stay
secondary visual elements.

## Verification

1. `npm run dev`, serve locally.
2. Playwright MCP: load page, screenshot desktop + mobile widths.
3. Confirm: 6 cards render in order; "Multiple" metric not broken; long metric values
   don't wrap badly; tech tags + highlights render; `#projects` anchor + smooth scroll
   intact.
4. `npm run build` passes.
