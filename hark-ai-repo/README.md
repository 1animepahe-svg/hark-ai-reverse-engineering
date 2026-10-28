# Hark AI — Reverse-Engineering Project

Public documentation of a static characterization of **Hark Pro** (`hark.com` / `hark.ai`) — an AI-assistant web product by Hark.

> Scope: passive, public-surface analysis only (HTML + shipped JavaScript). No authenticated accounts were accessed, no private credentials, no paid API keys. All findings come from what the site itself serves to any visitor.

## Artifacts

| File | What it is |
|---|---|
| [`hark-reverse-engineering-report.md`](./hark-report/hark-reverse-engineering-report.md) | Full findings report |
| [`docs/methodology.md`](./docs/methodology.md) | How the analysis was done (step by step) |
| [`docs/endpoints.md`](./docs/endpoints.md) | Live API surface inventory |
| [`docs/third-parties.md`](./docs/third-parties.md) | External service fingerprint table |

## Highlights

- **Stack:** Next.js App Router + Turbopack; 24 chunks, ~6.45 MB; **no source maps** shipped (minified-only analysis)
- **Unauthenticated live endpoint:** `GET /api/sky/iplocate` → `{city, latitude, longitude, timezone}` (geo-personalization, called at page load)
- **Pure relative-URL SPA:** zero `hark.*` host strings inside chunks — same-origin `/api/*` only
- **Deliberately thin third parties:** Sanity CDN, Cloudflare Insights beacon, one YouTube embed; no analytics SDKs detected
- **Security posture claims:** tokenized credential vault, watchable/cancellable agent actions ("open kitchen"), own-models-first inference, 0-retention vendor policy

## Ethics statement

This project documents publicly served frontend artifacts for educational/security-review purposes. It discloses no user data and no secret material that was not already public.
