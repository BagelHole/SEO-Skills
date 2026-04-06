# Google Search Console — Performance checklist

Use the **Performance** report for the correct property (domain or URL prefix). UI labels vary slightly; match by meaning.

## Queries tab (default search appearance / “Queries”)

1. Open **Performance** → ensure the date range matches what the user cares about (often **3 months** or **28 days**).
2. In the main chart area, enable metrics so you can see **CTR** and **average position** (e.g. click **Average CTR** and **Average position** so they appear in the table — exact control names may be “Total clicks”, “Total impressions”, “Average CTR”, “Average position”).
3. In the **queries** table (dimension = queries):
   - **Sort by Impressions** (descending) to find high-impression terms with weak CTR or poor position.
   - Increase **rows per page** to **50** or **100** if available.
4. Note patterns:
   - High impressions, **zero or very low clicks**, position roughly **5–15** → strong **title/meta** opportunity.
   - High impressions, **deep position** (e.g. 25+) → **content** or **intent** gap.
5. Optionally scan **Pages** filtered mentally by which queries point to which URLs (or switch to Pages tab next).

## Pages tab

1. Open the **Pages** tab (dimension = pages).
2. **Sort by Impressions** (descending).
3. Set **rows per page** to **50** or **100**.
4. For each high-impression URL, capture impressions, clicks, CTR, and position.
5. Scroll if needed; take additional snapshots rather than assuming one view shows everything.

## Edge cases

- **Property mismatch**: User may have both `www` and non-`www` or subdomain properties — use the property they verify in GSC.
- **Low data**: New sites may have sparse rows; widen the date range if the UI allows.
- **Filters**: If the user cares about a country or device, apply those filters and say so in the report.

## What to extract for the final report

- Top **queries** by impressions with CTR and position.
- Top **pages** by impressions with CTR and position.
- Clear list of URLs/queries for **Tier 1 / 2 / 3** in the output template.
