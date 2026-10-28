# API surface inventory — hark.com

## Verified live endpoints

| Method | Path | Auth | Response (observed) |
|---|---|---|---|
| GET | `/api/sky/iplocate` | none required | `{city, latitude, longitude, timezone}` — 2 decimal precision, IANA tz name |

Observed sample (from Ibadan mobile/ISP egress): `{"city":"Ibadan","latitude":7.38,"longitude":3.91,"timezone":"Africa/Lagos"}`

## Known internal surface (same-origin, relative-path)

The SPA references only same-origin relative `/api/*` routes; no absolute API hosts are embedded in any shipped chunk. The authenticated product API (agent execution, vault, persistence) is gated behind Google/Apple identity flows and is **out of scope** for this static project.

## Utility endpoints

| Purpose | Path |
|---|---|
| Geo lookup | `/api/sky/iplocate` |

## Static assets

| Kind | Path |
|---|---|
| Icons | `/images/favicon-dark.png`, `/images/favicon-light.png` |
| Bundles | `/_next/static/chunks/*.js?dpl=<deployment-id>` |
| CMS images | `https://cdn.sanity.io/images/w2mhvsaj/production/...` |
