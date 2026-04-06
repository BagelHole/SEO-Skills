---
name: bulk-seo-guides-from-keywords
description: >-
  Ships many SEO guide or landing pages using seo-work-brief.md from
  gsc-ahrefs-browser-audit: reads the New guide backlog section (queued rows by
  Priority), drafts substantive pages, updates routes, sitemap, and hub indexes.
  If the brief is missing, falls back to Ahrefs (browser when API/MCP quota is
  exhausted), optional web search for intent, then merges rows back into
  seo-work-brief.md. Batches of ~five pages, internal links, discovery surfaces
  beyond raw page files. Use for bulk new URLs, pSEO-style guides, or continued
  Ahrefs-driven expansion after rankings move.
license: MIT
compatibility: >-
  Requires a web app or static site codebase with routable pages, internet
  access, and either Ahrefs API/MCP or browser automation with user login.
  Large batches benefit from subagents or task queues if your agent supports
  them.
metadata:
  version: "1.0"
  source: claude-code-hearth-sessions-3d51460d
---

# Bulk SEO guides from keywords

## What this is

This skill encodes a **repeatable shipping loop** that improved rankings in practice: **research keywords → author many unique guides → register routes → update sitemap → list on resources/hub pages** so Google and users can find them. It complements **`gsc-ahrefs-browser-audit`** (writes the brief) and **`ctr-snippet-batch-optimize`** (snippet fixes on existing URLs).

## Input: `seo-work-brief.md` (preferred)

1. **Read `seo-work-brief.md`** at the site project root (default **`./seo-work-brief.md`**) unless the user gives another path. That file is produced by **`gsc-ahrefs-browser-audit`**; see [references/brief-format.md](references/brief-format.md) for how to parse it.
2. Use the section **`## New guide backlog (for bulk-seo-guides-from-keywords)`** as the **authoritative queue**: process rows with Status **`queued`** or empty, in **Priority** order.
3. After each batch, **edit the same `seo-work-brief.md`** and set **Status** to `shipped` or `skipped` for finished rows.
4. If the brief is **missing** or the backlog table is **empty**, fall through to the research phase below and optionally **create** a new `seo-work-brief.md` with a populated backlog for the next run.

## Research phase (fallback or top-up)

1. **Build or extend a candidate list** from Ahrefs **Organic keywords**, **Opportunities** (e.g. low-hanging fruit), or exported reports—prioritize **volume × realistic difficulty × fit** with the product.
2. **If API/MCP hits limits**, switch to **browser automation** with the user logged into Ahrefs (same rationale as the browser audit skill).
3. **Optional**: use web search (e.g. Exa or similar) to confirm **SERP intent** (informational vs tool vs mixed) before committing a template.
4. **Dedupe** against URLs that already exist in the repo (grep routes, sitemap, content folders).
5. When you used fallback research, **append or merge** new rows into **`seo-work-brief.md`** using the backlog table format from **`gsc-ahrefs-browser-audit/references/seo-work-brief.md`** so the queue stays the single source of truth.

## Page quality bar (non-negotiable)

- Each page needs **substantive, unique body content**—not spun placeholders. Include sections, examples, tables, or lists where appropriate.
- Add **internal links** to closely related existing guides (and note neighbors for future cross-links).
- Align **title and meta** with the target query using the same CTR habits as the **`ctr-snippet-batch-optimize`** skill’s `references/ctr-patterns.md` (same repo).

## Shipping phase (always complete the plumbing)

For **every** new URL, update whatever your stack uses—adapt names to the project:

| Step | Typical locations (examples) |
|------|-------------------------------|
| Page module | `pages/`, `resources/js/pages/`, `app/`, `content/` |
| Route registration | router config, `routes/*.php`, filesystem routes |
| Sitemap | static XML, `SitemapController`, `sitemap.ts`, host generator |
| Hub / index | “Resources”, “Guides”, footer sections, search index JSON |

**Do not** stop at “TSX created” if the user expects live URLs—confirm routes and sitemap are wired, or explicitly list remaining manual steps.

## Scale and execution

- **Batch size** — Groups of ~**5 pages** per iteration reduce context loss and review fatigue (adjust if the user asks).
- **Parallelism** — If the agent supports **subtasks/subagents**, parallelize batches; merge conflicts are avoided by giving each batch distinct filenames/slugs up front.
- **Slug consistency** — One slug per keyword cluster; avoid near-duplicate paths (e.g. `red-herring-examples` vs `red-herring-fallacy`) unless intent truly differs—document the distinction in copy.

## Handoff to the user

After a large batch, provide:

- **Full list of new paths** (domain-appended if they asked).
- Anything **left manual** (e.g. CDN cache, Search Console inspection).

## Related

- Produce or refresh the queue with **`gsc-ahrefs-browser-audit`** → **`seo-work-brief.md`**.
- Refresh snippets on thin-performing winners with **`ctr-snippet-batch-optimize`** (uses Tier tables in the same brief, not the backlog section).
- Backlog parsing rules: [references/brief-format.md](references/brief-format.md)
- Detailed checklist: [references/shipping-checklist.md](references/shipping-checklist.md)
