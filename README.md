# Drushim Scraper - Israel Job Listings from drushim.co.il

Extract structured data from [drushim.co.il](https://drushim.co.il) — structured job listings from drushim.co.il, Israel's leading job board. Search by keyword, location, category, experience level, and job type. Get full descriptions, salary data, company info, and geo-coordinates.

**[Run on Apify →](https://apify.com/blackfalcondata/drushim-scraper)**

---

## Key features

🔍 **Smart search with filters**

Search by keyword, location, and multiple filters. Smart input resolution ensures you always get results.

📄 **Detail enrichment**

Fetch full job descriptions, salary data, employer profiles, and contact information for each listing.

⚡ **Compact output for AI agents**

Core-fields-only mode optimized for MCP and AI agent workflows. Description truncation to control output size.

---

## Use cases

**Data pipeline automation**
Integrate with your ETL pipeline to collect structured listings from drushim.co.il on a schedule. Export to CSV, JSON, or directly to your database.

**Market research**
Monitor listings, track trends, and analyze market dynamics with structured, deduplicated data from drushim.co.il.

**AI and LLM workflows**
Use compact mode and description truncation to feed data into AI agents, MCP servers, and LLM pipelines without exceeding token budgets.

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

<!-- WRITE: 4-6 Q&A pairs relevant to this product -->

**Is it legal to scrape drushim.co.il?**
Web scraping of publicly available data is generally legal. This actor only accesses publicly visible information. Always check the target site's terms of service for your specific use case.

**How does incremental mode work?**
Each listing gets a content hash. On subsequent runs, only new or changed listings are emitted — saving time, compute, and storage.

---

## Known limitations

<!-- WRITE: 4-6 honest limitations -->

- <!-- WRITE: limitation 1 -->
- <!-- WRITE: limitation 2 -->

---

## Related products by Black Falcon Data

| Product | Description |
|:--------|:------------|
| [StepStone Jobs API](https://github.com/BlackFalconData-org/stepstone-jobs-api) | Job listings from 18 European portals |
| [Company Jobs Tracker](https://github.com/BlackFalconData-org/company-jobs-tracker-api) | Track new/removed jobs per company |
| [Indeed Jobs Feed](https://github.com/BlackFalconData-org/indeed-jobs-feed) | Indeed job listings with salary data |
| [Glassdoor Jobs Feed](https://github.com/BlackFalconData-org/glassdoor-jobs-feed) | Glassdoor listings with company ratings |
| [Arbeitsagentur Jobs Feed](https://github.com/BlackFalconData-org/arbeitsagentur-jobs-feed) | Germany's federal job portal (1M+ listings) |
| [Naukri Jobs Feed](https://github.com/BlackFalconData-org/naukri-jobs-feed) | India's largest job portal |
| [Bilbasen Scraper](https://github.com/BlackFalconData-org/bilbasen-scraper) | Denmark's largest car marketplace |

---

*Last updated: 2026 03*
