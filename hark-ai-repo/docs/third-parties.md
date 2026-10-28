# Third-party service fingerprints — hark.com

| Service | Domain / ID | Role | Notes |
|---|---|---|---|
| Sanity CMS | `cdn.sanity.io` — dataset `w2mhvsaj/production` | Content/images & marketing copy | imageSrcSet with `fm=webp` params |
| Cloudflare Insights | `cloudflareinsights.com` beacon | First-party web telemetry | CF hosting stack |
| YouTube | embed `0PSV7e1KawA` | Marketing video | Embedded player |

## Not present (HTTP surface)

- Sentry, PostHog, Amplitude, Segment, Mixpanel
- Clerk/Auth0/Supabase/Firebase auth SDKs (auth runs through native Google/Apple flows)
- Ad networks; no third-party trackers beyond the three services above

## Implication

Attack/analysis surface is unusually narrow: hosting layer (Cloudflare), CMS (Sanity), and first-party API. The heavy logic lives in same-origin chunks + authenticated-only flows.
