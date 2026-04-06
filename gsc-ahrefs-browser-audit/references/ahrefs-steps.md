# Ahrefs — Site Explorer checklist (browser)

Prerequisite: user is **signed in** with a plan that includes the needed reports. If not, stop and follow the main skill’s **authentication** instructions.

## Open Site Explorer

1. Navigate to **Site Explorer** for the target hostname.
2. Prefer **subdomains** (or the mode the user uses for their site) so you include `www` and apex consistently unless they specify otherwise.
3. Wait for **overview** metrics to load (DR, organic keywords, traffic estimates, etc.). Use short waits + fresh snapshots if the UI is slow.

## Overview

Capture high-level numbers the UI shows, for example:

- Domain Rating (DR) and trend if visible  
- Organic keywords count and growth  
- Organic traffic estimate  
- Referring domains / backlinks (if relevant to recommendations)

Exact widgets depend on Ahrefs version; **record what you see**, not a fixed schema.

## Organic keywords

1. Open **Organic keywords** (or equivalent) from the Site Explorer sidebar or overview links.
2. **Token / size warning**: full keyword tables can be enormous. If automation returns oversized output or errors:
   - Apply **filters** (e.g. position bucket, volume minimum, SERP features).
   - Sort by **volume** or **traffic** and summarize **top N rows** visible on screen.
   - Use **pagination** or narrower country/language instead of dumping the entire table.
3. Note **quick wins**: keywords ranking roughly **4–15** with decent volume (aligns with “low-hanging fruit” elsewhere).

## Opportunities

1. Open **Opportunities** (or similarly named report) if available on the account.
2. Review buckets such as **low-hanging fruit** (positions ~4–15), **content gaps**, etc., depending on what Ahrefs shows.
3. If results are **geo-filtered** (e.g. United States only) and look empty, try **All locations** (or global), then apply **Show results** / refresh so the table repopulates.

## Other useful areas (time permitting)

- **Top pages** — which URLs earn traffic and keywords.  
- **Content gap** — vs competitors (only if the user cares and data loads).  
- **Site structure / internal** — if visible and useful for internal linking advice.

Do **not** treat API or MCP as required; browser session is the source of truth for this skill.

## Auth and session issues

- **Signed out**, **session exceeded**, or **multiple devices**: pause for the user; they may need to sign in again or free a session.
- After login, **re-navigate** to Site Explorer with the correct `target=` hostname.
