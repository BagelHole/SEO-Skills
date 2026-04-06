# SEO work brief (`seo-work-brief.md`)

This file is the **single markdown artifact** the audit produces on disk and that **`bulk-seo-guides-from-keywords`** reads for the **new guide backlog**. Keep it in the **root of the site project** being optimized (not inside the SEO-Skills repo unless that is the site).

## File placement

- **Default path:** `./seo-work-brief.md` (repository root of the product site).
- **Override:** If the user asks for another path, use it and tell **`bulk-seo-guides-from-keywords`** where it lives.

Optional YAML front matter (helps humans and agents):

```yaml
---
brief_version: 1
site: "example.com"
generated: "2026-04-06"
gsc_date_range: "Last 3 months"
ahrefs_scope: "All locations"
---
```

# Body template

## SEO work brief — {hostname}

### Executive summary

2–4 sentences: biggest lever and the single highest-ROI next step.

### Overall metrics

| Metric | Value | Notes |
|--------|--------|--------|
| GSC clicks / impressions / CTR / avg position | … | Date range |
| Ahrefs DR | … | If used |
| Ahrefs organic keywords / traffic est. | … | If used |
| Referring domains | … | If visible |

### Tier 1 — High impressions, zero (or near-zero) CTR

Priority for **title + meta** rewrites (`ctr-snippet-batch-optimize`).

| Page or query | Impressions | Clicks | CTR | Position | Priority |
|---------------|-------------|--------|-----|----------|----------|
| … | … | … | … | … | Critical / High |

### Tier 2 — Meaningful impressions but low CTR

| Page | Impressions | Clicks | CTR | Position |
|------|-------------|--------|-----|----------|
| … | … | … | … | … |

### Tier 3 — High impressions, deep positions

| Page | Impressions | Position | Opportunity |
|------|-------------|----------|-------------|
| … | … | … | Expand / consolidate / etc. |

### Ahrefs keyword / opportunity highlights

If Ahrefs was used:

| Keyword / theme | Volume | KD | Current pos | Target page |
|-----------------|--------|-----|-------------|-------------|
| … | … | … | … | … |

If Ahrefs was **skipped**: *Ahrefs not used (reason).*

### Recommended action plan

1. …

---

## New guide backlog (for bulk-seo-guides-from-keywords)

**Required heading** — use this exact text so the bulk skill can find it.

Populate from Ahrefs **Organic keywords**, **Opportunities**, and content gaps. One row per **new** URL to create (not Tier 1–3 snippet fixes on existing pages).

| Priority | Primary keyword | Volume | KD | Intent | Suggested slug | Notes | Status |
|----------|-----------------|--------|-----|--------|----------------|-------|--------|
| 1 | … | … | … | informational / commercial / mixed | guides/example-topic | … | queued |

**Columns**

- **Priority** — Integer; **lower runs first** when batching.
- **Primary keyword** — Main query the page should satisfy.
- **Volume / KD** — From Ahrefs when available; else `—`.
- **Intent** — Short SERP intent note.
- **Suggested slug** — Path segment or full path (no domain), e.g. `guides/verisimilitude`.
- **Notes** — Opportunity bucket, internal link ideas, or “avoid duplicate of `/guides/x`”.
- **Status** — `queued` (default for new rows), `shipped`, or `skipped`. The bulk skill only consumes **`queued`** or **empty** cells.

After each shipping batch, **update Status** to `shipped` for completed rows so reruns do not duplicate work.
