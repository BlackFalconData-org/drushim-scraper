# Drushim Scraper - Israel Job Listings from drushim.co.il

Extract structured data from [drushim.co.il](https://drushim.co.il) — structured job listings from drushim.co.il, Israel's leading job board. Search by keyword, location, category, experience level, and job type. Get full descriptions, salary data, company info, and geo-coordinates.

**[Drushim Scraper - Israel Job Listings on Apify →](https://apify.com/blackfalcondata/drushim-scraper)**

---

## Key features




**Search with filters** — Search by keyword and location. Filter by category, region, job scope, and more.

**Detail enrichment** — Fetch full job descriptions, salary data, direct apply URLs for each listing.

**Incremental mode** — Only get new or changed listings since your last run. Content hash per listing — no duplicates, no re-processing.

---

## Use cases




**Data pipeline automation**
Integrate with your ETL pipeline to collect structured listings from drushim.co.il on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor listings, track trends, and analyze market dynamics with structured, deduplicated data from drushim.co.il.

---

## Quick start

```json
{
  "query": "developer",
  "maxResults": 50,
  "includeDetails": true
}
```

---

## Input parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `query` | string | — | Job search keywords (Hebrew or English). Use JSON array for multi-query, e.g. ["developer", "מפתח"]. |
| `location` | string | — | City name (Hebrew or English). Resolved to geo-coordinates via Drushim autocomplete. Use JSON array for multi-location. |
| `maxResults` | integer | `50` | Maximum job listings to return. 0 = unlimited. |
| `maxPages` | integer | `10` | Maximum search result pages per query. |
| `category` | enum | — | Job category code. |
| `subCategory` | integer | — | Sub-category code within the selected category. The available codes depend on the parent category — check drushim.co.il for valid values. |
| `area` | enum | — | Geographic region filter. |
| `scope` | enum | — | Employment scope / work arrangement. |
| `experience` | enum | — | Required experience level. |
| `noCvRequired` | boolean | `false` | Only show jobs that don't require uploading a CV. |
| `includeDetails` | boolean | `true` | Include full HTML description and requirements in output. Disable for smaller output. |
| `descriptionMaxLength` | integer | `0` | Truncate plain-text description to this many characters. 0 = no truncation. |
| `compact` | boolean | `false` | Output only core fields (for AI-agent/MCP workflows). |

---

## FAQ

**Is it legal to scrape drushim.co.il?**
Web scraping of publicly available data is generally legal. This actor only accesses publicly visible information. Always check the target site's terms of service for your specific use case.

**How does incremental mode work?**
Each listing gets a content hash. On subsequent runs, only new or changed listings are emitted — saving time, compute, and storage.

**What languages are supported for search queries?**
Both Hebrew and English queries are supported. Location names can be entered in Hebrew or English — the actor resolves them via the Drushim autocomplete API to ensure accurate geo-coordinates.

**Can I filter by remote or part-time work?**
Yes. The `scope` filter supports full-time, part-time, remote, hybrid, and freelance options. Combine with `area` and `experience` filters for precise targeting.

**How much does it cost to run?**
Pricing is pay-per-event: $0.01 per run start + $0.002 per result. Fetching 1,000 job listings costs approximately $2.01 in compute events. Actual Apify platform costs (memory, CPU) are additional and depend on run size.

**Can I use this with AI agents or MCP workflows?**
Yes. Enable `compact: true` to receive only core fields, and set `descriptionMaxLength` to cap description length. This keeps token usage predictable when piping data into LLM pipelines or MCP servers.

**Does the actor return salary information?**
Yes, when the listing includes salary data. Fields `salaryMin`, `salaryMax`, `salaryCurrency`, and `salaryPeriod` are always present in the output — populated when drushim.co.il provides salary data for the listing, null otherwise.

---

## Known limitations

- **Hebrew content encoding** — Job titles, company names, and locations are returned in Hebrew script as published by drushim.co.il. English transliterations are not provided for fields that the site only publishes in Hebrew.
- **Sub-category codes are undocumented** — The `subCategory` filter accepts numeric codes that vary per parent category. Valid codes must be looked up manually on drushim.co.il; there is no programmatic enumeration available.
- **No historical data** — The actor scrapes current listings only. Jobs that have been removed from drushim.co.il are not accessible; incremental mode detects removals only if you maintain your own snapshot.
- **Salary coverage is partial** — Not all listings include salary data. The `salaryMin`/`salaryMax` fields will be null for listings where the employer has not disclosed compensation.
- **No applicant tracking** — The actor extracts listing data only. It does not submit applications, track application status, or interact with the apply flow beyond surfacing the `applyUrl` field.
- **Rate sensitivity** — Very large runs (tens of thousands of results) may encounter rate limits from drushim.co.il. Use `maxResults` and `maxPages` to scope runs appropriately.

---

## Related products by Black Falcon Data




- [StepStone Scraper](https://github.com/BlackFalconData-org/stepstone-scraper) — Job listings from 18 European portals
- [Indeed Job Scraper](https://github.com/BlackFalconData-org/indeed-job-scraper) — Indeed job listings with salary data
- [Glassdoor Job Scraper](https://github.com/BlackFalconData-org/glassdoor-job-scraper) — Glassdoor listings with company ratings

---

*Last updated: 2026 03*
