# Methodology — Hark (hark.com) static characterization

## 1. Surface capture
1. `GET https://hark.com/` — full HTML (165 KB) saved.
2. Extracted all `<script src>` / `<link href>` ending in `.js` → **24 unique chunks** under `/_next/static/chunks/*.js?dpl=dpl_43vpACitAoHemg5zATXXCP8hBYHa`, all fetched with the deployment parameter.
3. Stored a byte-for-byte mirror (`app/index.html` + `app/_next/static/chunks/*.js`, 6.45 MB) for analysis.

## 2. Static analysis
- Regex/string sweeps over the mirrored corpus for: absolute URLs (`https://…`), WebSocket schemes (`wss://`), internal API paths (`/api/…`), SDK fingerprints (`sentry`, `posthog`, `amplitude`, `segment`, `supabase`, `clerk`, `firebase`, …), source-map markers (`sourceMappingURL`).
- Result: `mapRefs=0` → **no source maps served** → minified-only analysis.
- Targeted REA pass (`rea-agents` `analyze-javascript-application`) for module-graph/inventory extraction.

## 3. Endpoint probing (passive)
- Single unauthenticated `GET /api/sky/iplocate` to read response shape (`200 application/json`, `{city, latitude, longitude, timezone}`).
- Route inventory captured from anchor tags mirrored in HTML: `/manifesto /security /articles /careers /contact-hark /pricing /privacy-policy /terms /using-hark /other-policies`.

## 4. Third-party fingerprinting
- Host strings and script/link domains enumerated; classified by function (CMS, telemetry, video).
- Marker histogram for common analytics SDK names → **zero hits** on the HTML surface.

## Limits
- Minified bundles: identifier mapping unavailable without source maps.
- Authenticated product surface (agent chat + vault APIs) not reachable without an account session — intentionally not attempted.
