---
name: ctr-snippet-batch-optimize
description: >-
  Batch-rewrites page titles, meta descriptions, and matching on-page headlines
  (including JSON-LD where the site duplicates the title) using tiers from
  Google Search Console data—prioritizing high impressions with zero or low CTR
  on page 1–2, then deeper positions. Encodes repeatable CTR patterns from
  production workflows: numbers and list counts in titles, bracket qualifiers,
  question-led descriptions, concrete examples, deduped title phrasing, and
  current-year refresh on time-sensitive pages. Use after a GSC audit or
  alongside gsc-ahrefs-browser-audit output when the user wants implementation,
  not just research. Trigger when the user mentions batch title tags, meta
  rewrites, GSC tiers, zero-CTR pages, snippet optimization, or SEOLayout-style
  title/description updates across many URLs.
license: MIT
compatibility: >-
  Requires access to the site codebase (React/Vue/Blade/etc.). No browser
  required unless you are still gathering GSC data. Respect the project’s
  existing SEO component conventions (e.g. layout props, head manager, CMS
  fields).
metadata:
  version: "1.0"
  source: claude-code-hearth-sessions-657b0567
---

# CTR snippet batch optimize (from GSC tiers)

## What this is

This skill implements **what worked in practice**: after you know which URLs underperform in **Search Console**, you **batch-update titles, meta descriptions, and schema/article headlines** so they match intent and earn clicks. It is the **implementation** complement to research skills such as **`gsc-ahrefs-browser-audit`** (which produces the tier lists).

## Inputs you need

Either:

- **`seo-work-brief.md`** at the site project root (from **`gsc-ahrefs-browser-audit`**) — use the **Tier 1–3** tables and ignore the **`## New guide backlog`** section (that section is for **`bulk-seo-guides-from-keywords`**), **or**
- Any other finished report with **URL paths**, **impressions**, **clicks**, **CTR**, **position**, **or**
- Instructions to **run or reuse** a GSC Performance export / audit first, then proceed.

## Tiering (use the same logic as the winning workflow)

| Tier | Signal | Primary lever |
|------|--------|----------------|
| **1** | High impressions, **~0% CTR**, position roughly **5–15** (page 1–2) | **Title + meta** rewrite (biggest ROI) |
| **2** | Page 1–2 but **CTR clearly below** typical band for that position | Title + meta; check weak intent match |
| **3** | High impressions but **deep position** (e.g. 25+) | Meta tuned for future lift; **content depth** and internal links matter more than the snippet alone |

Sort work **by impressions within each tier** so the largest gaps are addressed first.

## Execution steps

1. **Normalize URLs** — Strip domain to paths (e.g. `/guides/example`) so you can search the repo.
2. **Locate files** — Grep/route tables/CMS map: find the component or template that sets `<title>`, meta description, and any **schema `headline`** that mirrors the title.
3. **Read before edit** — Batch-read the relevant files (or the shared layout wrapper) so you do not fight per-page conventions.
4. **Apply patterns** — Follow [references/ctr-patterns.md](references/ctr-patterns.md) on every targeted page unless a pattern would misrepresent the content.
5. **Keep schema and UI in sync** — If the page exposes `headline` / `title` in JSON-LD or hero H1 from the same string source, **update once** in the canonical place or update all mirrors consistently.
6. **Verify** — Spot-check a few pages in the dev server; ensure no duplicate `<title>` boilerplate (e.g. “Examples: Definition and Examples”).

## Scope control

- If the user names a **maximum page count**, respect it (e.g. top 20 Tier 1 only).
- **Do not** invent traffic numbers; use only figures from the supplied audit or freshly pulled GSC data.
- **Do not** keyword-stuff or promise medical/legal/financial outcomes in snippets.

## Related

- Research and tier scaffolding: skill **`gsc-ahrefs-browser-audit`** (same repo).
- Pattern cheat sheet: [references/ctr-patterns.md](references/ctr-patterns.md)
