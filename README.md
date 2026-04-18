# Drushim Scraper - Israel Job Listings from drushim.co.il

Extract structured data from [drushim.co.il](https://drushim.co.il) — structured job listings from drushim.co.il, Israel's leading job board. Search by keyword, location, category, experience level, and job type. Get full descriptions, salary data, company info, and geo-coordinates.

**[Drushim Scraper - Israel Job Listings on Apify →](https://apify.com/blackfalcondata/drushim-scraper?fpr=1h3gvi)**

---

## Key features





**Search with filters** — Search by keyword and location. Filter by category, region, job scope, and more.

**Detail enrichment** — Fetch full job descriptions, salary data, direct apply URLs for each listing.

**Incremental mode** — Only get new or changed listings since your last run. Content hash per listing — no duplicates, no re-processing.

**Compact output** — Emit core fields only (AI-agent / MCP-friendly). Keeps response size small for LLM workflows.

**Description truncation** — Cap description length per listing to control output size and cost.

**Result cap** — Stop after N listings (up to 5.000). Set to 0 for the full catalog.

**Export anywhere** — Download as JSON, CSV, or Excel. Stream via Apify API, webhooks, or integrations with Make, Zapier, Airbyte, Keboola.

**Structured data** — Every listing returns the same schema with consistent field naming. All fields always present — `null` when unavailable, never omitted.

---

## Use cases





**Data pipeline automation**
Integrate with your ETL pipeline to collect structured listings from drushim.co.il on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor listings, track trends, and analyze market dynamics with structured, deduplicated data from drushim.co.il.

**Change monitoring**
Run daily or hourly in incremental mode to capture only new, updated, or expired listings. Perfect for price-tracking, churn analysis, and alerting pipelines.

**Compensation benchmarking**
Aggregate salary ranges across roles, industries, and locations on drushim.co.il to inform pricing decisions, hiring plans, or candidate negotiations.

**AI / LLM training data**
Structured JSON per listing is ready for RAG pipelines, embeddings, and agent workflows. Compact mode trims tokens for LLM context windows.

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


## Output fields

Every listing returns the same 37-field schema. Missing values are `null` — never omitted.

- `jobId`
- `jobCode`
- `title`
- `company`
- `companyCode`
- `companyLogoUrl`
- `companyProfileUrl`
- `location`
- `locationEnglish`
- `region`
- `regionEnglish`
- `latitude`
- `longitude`
- `description`
- `descriptionHtml`
- `requirements`
- `requirementsHtml`
- `descriptionLength`
- `salary`
- `salaryText`
- `category`
- `subCategory`
- `experience`
- `experienceCode`
- `employmentType`
- `scopes`
- `benefits`
- `isRemote`
- `isHybrid`
- `isSponsored`
- `isHot`
- `isExpired`
- `portalUrl`
- `applyUrl`
- `postedDate`
- `scrapedAt`
- `searchQuery`


## Sample output

One object per listing. Here is a real example from a production run:

```json
{
  "jobId": "drushim-36398645",
  "jobCode": 36398645,
  "title": "(RG) Senior Full Stack Developer",
  "company": "Elad Software",
  "companyCode": 6390,
  "companyLogoUrl": "https://webapi.drushim.co.il/logos/6390/page/637296316494898491.png",
  "companyProfileUrl": "https://www.drushim.co.il/דרושים-6390-elad-group/",
  "location": "ראשון לציון",
  "locationEnglish": "\tRishon LeTsiyon\t",
  "region": "מרכז",
  "regionEnglish": "Center",
  "latitude": 31.9730015
}
```

*Truncated — full records contain 37 fields. See Output fields for the complete schema.*


**[Try Drushim Scraper - Israel Job Listings now — $5 free credit, no credit card →](https://apify.com/blackfalcondata/drushim-scraper?fpr=1h3gvi)**


## Pricing

Pay only for what you extract. No subscription required — Apify's free $5 credit covers thousands of results.

| Event | Price (USD) |
| --- | --- |
| Actor Start | $0.01 |
| Result | $0.002 |

See the [actor on Apify](https://apify.com/blackfalcondata/drushim-scraper?fpr=1h3gvi) for current pricing.

---

## Related products by Black Falcon Data





- [StepStone Scraper](https://apify.com/blackfalcondata/stepstone-scraper?fpr=1h3gvi) — Job listings from 18 European portals
- [Indeed Job Scraper](https://apify.com/blackfalcondata/indeed-job-scraper?fpr=1h3gvi) — Indeed job listings with salary data
- [Glassdoor Job Scraper](https://apify.com/blackfalcondata/glassdoor-job-scraper?fpr=1h3gvi) — Glassdoor listings with company ratings
- [Arbeitsagentur Scraper](https://apify.com/blackfalcondata/arbeitsagentur-scraper?fpr=1h3gvi) — Germany's official job portal (1M+ listings)
- [SEEK Scraper](https://apify.com/blackfalcondata/seek-scraper?fpr=1h3gvi) — Australia & NZ's largest job board
- [Naukri Scraper](https://apify.com/blackfalcondata/naukri-scraper?fpr=1h3gvi) — India's largest job portal


## Getting started with Apify

New to Apify? [Create a free account with $5 credit](https://console.apify.com/sign-up?fpr=1h3gvi) — no credit card required.

1. [Sign up free](https://console.apify.com/sign-up?fpr=1h3gvi) — $5 credit included
2. Open the actor and paste your input
3. Click Start — results download as JSON, CSV, or Excel

Need more volume? [See pricing](https://apify.com/pricing?fpr=1h3gvi).

---


## About Black Falcon Data

Black Falcon Data builds production-grade web scrapers for job boards and marketplace data. Browse our full actor catalog at [www.blackfalcondata.com](https://www.blackfalcondata.com).

---
---

*Last updated: 2026 03*
