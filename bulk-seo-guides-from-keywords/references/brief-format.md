# Input: `seo-work-brief.md`

## Default location

Read **`./seo-work-brief.md`** at the **site project root** first. If the user passes another path, use that.

## Section to consume

Find the heading (exact text):

```text
## New guide backlog (for bulk-seo-guides-from-keywords)
```

Parse the **markdown table** immediately below it.

## Row selection

Process rows where **Status** is:

- `queued`, or
- empty / missing

Skip rows marked **`shipped`** or **`skipped`**.

## Sort order

Sort by **`Priority`** ascending (1 before 2). Tie-break by row order in the file.

## After shipping

Update the brief in place: set **Status** to `shipped` (or `skipped` with a short reason) for each completed row so future runs do not recreate the same URLs.

## Full brief spec

The audit skill defines the complete file shape and column meanings: **`gsc-ahrefs-browser-audit/references/seo-work-brief.md`** (same repository as these skills).

If **`seo-work-brief.md`** is missing or the backlog table is empty, fall back to live Ahrefs (or browser) research and offer to **create** a new brief with a populated backlog for the next run.
