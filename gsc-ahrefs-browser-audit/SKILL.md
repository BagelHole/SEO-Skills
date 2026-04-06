---
name: gsc-ahrefs-browser-audit
description: >-
  Runs a deep SEO research pass using the user’s logged-in Google Search Console
  and Ahrefs sessions in a real browser (not API-first). Discovers the site
  domain from the project or user input, extracts Performance queries and pages
  (impressions, clicks, CTR, position), then Ahrefs Site Explorer (overview,
  organic keywords, Opportunities such as low-hanging fruit) to find CTR,
  ranking, and impression improvements. Pauses for manual sign-in when needed;
  skips Ahrefs if there is no access. Writes seo-work-brief.md for downstream
  bulk guide shipping. Use when the user asks for GSC analysis, Search Console
  audits, Ahrefs research, organic keyword opportunities, CTR fixes, or
  impression growth plans.
license: MIT
compatibility: >-
  Requires browser automation (any MCP or tool your agent provides), internet
  access, and interactive login to Google and optionally Ahrefs. Iframe-only UI
  regions are not automatable. Ahrefs API/MCP is optional; prefer browser when
  rate limits apply.
metadata:
  version: "1.0"
  source: transcript-2026-04-06
---

# GSC + Ahrefs browser SEO audit

## Goal

Produce actionable findings to improve **CTR**, **rankings**, and **impressions** by combining:

1. **Google Search Console** — Performance report (queries + pages).
2. **Ahrefs** (optional) — Site Explorer, organic keywords, and **Opportunities**.

Use **browser automation** with the **user’s own logged-in sessions**. Prefer this over Ahrefs API or Ahrefs MCP when those hit **rate limits** quickly; the browser carries normal UI quota and features.

## Tools

Use whatever **browser automation** your environment exposes (e.g. Playwright MCP, Cursor IDE browser tools). Names and refs differ by product; always take a **fresh snapshot** after navigation or login before clicking.

## Before you start: resolve the site

Determine the **canonical hostname** (e.g. `example.com`) before building URLs. Order of inference:

1. User explicitly states the domain or URL.
2. Environment variables: `SITE_URL`, `CANONICAL_URL`, `NEXT_PUBLIC_SITE_URL`, `VERCEL_URL` (normalize to hostname).
3. `package.json` — `homepage`, or `repository.url` if it is a production site URL.
4. Framework config — e.g. Next.js `metadataBase` / `siteUrl` in config, Astro `site`, etc.
5. Project `README.md`.
6. If still unclear, **ask the user** for the domain and whether the GSC property is **Domain** or **URL prefix**.

**GSC deep link (domain property):**

`https://search.google.com/search-console/performance/search-analytics?resource_id=sc-domain%3A{hostname}`

For **URL-prefix** properties, open Search Console and let the user select the property (see authentication below); do not guess `resource_id`.

**Ahrefs Site Explorer (subdomains mode, adjust if user prefers path or exact URL):**

`https://app.ahrefs.com/site-explorer/overview/v2/subdomains/live?target={hostname}`

(Older `/v2/site-explorer/overview?target=...&mode=subdomains` may redirect; either is fine.)

## Authentication: wait for the user

**Never ask for passwords or 2FA codes.** If the page shows login, account picker, “session limit exceeded,” or paywall:

1. **Stop** automated clicks that assume a logged-in dashboard.
2. **Tell the user** exactly what you see and what they should do (sign in, pick property, dismiss other sessions).
3. **Wait** until they confirm or until a new snapshot shows the expected logged-in view.
4. **Resume** with a fresh navigation to the target URL if needed.

Repeat for **GSC** and **Ahrefs** independently.

## If Ahrefs is unavailable

If there is no subscription, paywall, or the user opts out: complete the **GSC-only** analysis, state clearly that Ahrefs was skipped, and still deliver tiers and recommendations from GSC.

## Execution order

1. Resolve hostname → open GSC Performance (or property chooser).
2. Complete [GSC steps](references/gsc-steps.md): queries dimension, then pages.
3. Open Ahrefs Site Explorer for the same hostname (after login if required).
4. Complete [Ahrefs steps](references/ahrefs-steps.md): overview, organic keywords (summarize safely), Opportunities, location filters as needed.
5. Synthesize the report and **write the on-disk brief** (see Output below).

## Large pages and token limits

Ahrefs **Organic keywords** and similar views can return **huge** snapshots. If tool output is truncated or errors on size:

- Rely on **visible rows**, **filters**, **sorts**, and **pagination** instead of one full-table scrape.
- Summarize **top N** by volume or position bands.
- Use **Opportunities** views for pre-bucketed lists.

## Output

1. **Write `seo-work-brief.md`** to the **root of the site repository** you audited (default path `./seo-work-brief.md`). If the user wants a different path or filename, use theirs and mention it in the brief’s top lines.
2. Follow [references/seo-work-brief.md](references/seo-work-brief.md) for the full structure: metrics, Tier 1–3 tables, Ahrefs highlights, action plan, and the **`## New guide backlog (for bulk-seo-guides-from-keywords)`** section with the backlog table populated from keyword research (new pages only).
3. You may **also** give a short summary in chat, but the **markdown file is the source of truth** for the next step (`bulk-seo-guides-from-keywords`).

Quick pointer: [references/output-template.md](references/output-template.md) (on-disk brief reminder).

## Implementation follow-up (separate task)

If the user asks you to **change titles, meta descriptions, or content** in their codebase, treat that as **implementation**: map GSC/Ahrefs URLs to routes/files **in that project** using normal repo search. For **batched snippet rewrites from tier lists**, use the **`ctr-snippet-batch-optimize`** skill in this repo. This skill focuses on **research and reporting** unless the user explicitly asks for edits.

## Reference files

| File | Purpose |
|------|--------|
| [references/gsc-steps.md](references/gsc-steps.md) | Click-path checklist for Performance |
| [references/ahrefs-steps.md](references/ahrefs-steps.md) | Site Explorer and Opportunities |
| [references/seo-work-brief.md](references/seo-work-brief.md) | Full `seo-work-brief.md` spec + backlog for bulk guides |
| [references/output-template.md](references/output-template.md) | Pointer: write brief to disk, not chat-only |
