# Intermediair Scraper - Dutch professional job board

Extract structured data from [intermediair.nl](https://intermediair.nl) — intermediair.nl - the Netherlands' leading professional job board. Every result ships with recruiter contact details, structured salary min/max ranges, and rich filtering across six job dimensions.

**[Intermediair Scraper - Dutch professional job board on Apify →](https://apify.com/blackfalcondata/intermediair-scraper?fpr=1h3gvi)**

---

## Key features

**Search with filters** — Search by keyword and location. Filter by country, sort, and more.

**Detail enrichment** — Fetch full job descriptions, salary data, employer profiles, contact information for each listing.

**Incremental mode** — Only get new or changed listings since your last run. Content hash per listing — no duplicates, no re-processing.

**Change classification** — Track unchanged, expired, cross-run repost detection across runs. Build audit trails of how listings evolve over time.

**Compact output** — Emit core fields only (AI-agent / MCP-friendly). Keeps response size small for LLM workflows.

**Description truncation** — Cap description length per listing to control output size and cost.

**Result cap** — Stop after N listings (up to 1.000). Set to 0 for the full catalog.

**Export anywhere** — Download as JSON, CSV, or Excel. Stream via Apify API, webhooks, or integrations with Make, Zapier, Airbyte, Keboola.

**Structured data** — Every listing returns the same schema with consistent field naming. All fields always present — `null` when unavailable, never omitted.

---

## Use cases

**Data pipeline automation**
Integrate with your ETL pipeline to collect structured listings from intermediair.nl on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor listings, track trends, and analyze market dynamics with structured, deduplicated data from intermediair.nl.

**Change monitoring**
Run daily or hourly in incremental mode to capture only new, updated, or expired listings. Perfect for price-tracking, churn analysis, and alerting pipelines.

**Compensation benchmarking**
Aggregate salary ranges across roles, industries, and locations on intermediair.nl to inform pricing decisions, hiring plans, or candidate negotiations.

**Lead generation**
Extract employer contact details alongside listings to build outreach lists for recruiters, staffing agencies, or B2B sales teams.

**AI / LLM training data**
Structured JSON per listing is ready for RAG pipelines, embeddings, and agent workflows. Compact mode trims tokens for LLM context windows.

---

## Quick start

```json
{
  "query": "software developer",
  "location": "Amsterdam",
  "maxResults": 10,
  "includeDetails": true
}
```

---

## Input parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `query` | string | — | Job search keywords. |
| `country` | enum | `"NL"` | Which market to search. |
| `location` | string | — | City or place name, resolved through Intermediair's address service. |
| `radiusKm` | integer | `40` | Search radius around the resolved location. |
| `sort` | enum | `"relevance"` | Result ordering. |
| `maxResults` | integer | `25` | Maximum total results (0 = unlimited). |
| `includeDetails` | boolean | `false` | Fetch full detail records for each job for enrichment and parity across runs. Disabled by default because search results already include the full useful payload. |
| `descriptionMaxLength` | integer | `0` | Truncate description to N chars. 0 = no truncation. |
| `compact` | boolean | `false` | Core fields only (for AI-agent/MCP workflows). |
| `incrementalMode` | boolean | `false` | Compare against previous run state. |
| `stateKey` | string | — | Stable identifier for tracked universe. |
| `emitUnchanged` | boolean | `false` | Also emit jobs that have not changed since the last run (incrementalMode only). |
| `emitExpired` | boolean | `false` | Also emit jobs that have disappeared since the last run (incrementalMode only). |
| `contractType` | string | — | Filter by contract type. Use the exact Intermediair term (e.g. "Vast", "Tijdelijk", "Freelance"). |
| `educationLevel` | string | — | Filter by minimum education level (e.g. "HBO", "WO", "MBO"). |
| `careerLevel` | string | — | Filter by career level (e.g. "Ervaren", "Starter", "Senior"). |
| `industry` | string | — | Filter by industry. Use the exact Intermediair value, including slash forms where applicable (e.g. "Overheid/Non-profit", "ICT"). |
| `category` | string | — | Filter by job category. Use the exact parent/sub value from Intermediair's category list (e.g. "Financieel/Accounting", "ICT/Softwareontwikkeling"). Unknown values are rejected. |
| `workingPlace` | string | — | Filter by work location style (e.g. "Hybride", "Op locatie", "Thuis"). |
| `skipReposts` | boolean | `false` | Exclude jobs detected as reposts of previously seen listings. |

---

## Output fields

Every listing returns the same 53-field schema. Missing values are `null` — never omitted.

- `jobId`
- `title`
- `functionTitle`
- `company`
- `companyType`
- `companyUrl`
- `location`
- `city`
- `municipality`
- `zipCode`
- `province`
- `countryCode`
- `latitude`
- `longitude`
- `description`
- `descriptionHtml`
- `descriptionMarkdown`
- `contractType`
- `salaryText`
- `salaryMin`
- `salaryMax`
- `salaryCurrency`
- `salaryType`
- `employmentType`
- `careerLevel`
- `educationLevel`
- `categories`
- `industries`
- `workingPlace`
- `hours`
- `workingHoursMin`
- `workingHoursMax`
- `postedAt`
- `validThrough`
- `url`
- `applyUrl`
- `portalUrl`
- `contactName`
- `email`
- `phone`
- `companyWebsite`
- `recruiterId`
- `referenceId`
- `numberOfApplies`
- `isRepost`
- `repostOfId`
- `repostDetectedAt`
- `searchQuery`
- `contentQuality`
- `detailFetched`
- `scrapedAt`
- `source`
- `changeType`

---

## Sample output

One object per listing. Here is a real example from a production run:

```json
{
  "jobId": "3760dfa3b2ede40864a8188f8ae8db79b77424f3c1c3de663039fcd4bf6728ba",
  "title": "Finance Manager | Financieel Manager",
  "functionTitle": "Finance Manager | Financieel Manager",
  "company": "Randstad Professional",
  "companyType": "human_resource_manager",
  "companyUrl": null,
  "location": "Amersfoort",
  "city": "Amersfoort",
  "municipality": "AMERSFOORT",
  "zipCode": "3811AA",
  "province": "Utrecht",
  "countryCode": "NL"
}
```

*Truncated — full records contain 53 fields. See Output fields for the complete schema.*

**[Try Intermediair Scraper - Dutch professional job board now — $5 free credit, no credit card →](https://apify.com/blackfalcondata/intermediair-scraper?fpr=1h3gvi)**

---

## Pricing

Pay only for what you extract. No subscription required — Apify's free $5 credit covers thousands of results.

| Event | Price (USD) |
| --- | --- |
| Actor Start | $0.00005 |
| Result | $0.0015 |

See the [actor on Apify](https://apify.com/blackfalcondata/intermediair-scraper?fpr=1h3gvi) for current pricing.

---

## FAQ

**How do I scrape intermediair.nl?**
Use this actor on Apify to extract structured data from intermediair.nl. Configure your search query and filters in the input, then click Start — no coding required.

**How do I get intermediair.nl data as JSON, CSV, or Excel?**
The actor writes each listing to Apify's dataset. Download as JSON, CSV, or Excel from the Console, stream via the API, or push to Make, Zapier, Airbyte, or Keboola.

**Is it legal to scrape intermediair.nl?**
Web scraping of publicly available data is generally legal. This actor only accesses publicly visible information. Always check intermediair.nl's terms of service for your specific use case.

**How much does it cost?**
Pay-per-event pricing — you only pay for listings extracted. Apify's free $5 credit is enough to run thousands of results before you pay anything.

**How does incremental mode work?**
Each listing gets a content hash. On subsequent runs, only new or changed listings are emitted — saving time, compute, and storage. Expired listings can be tracked separately.

**Do I need an API key or credentials?**
No. Just sign up for Apify, paste your input, and click Start. No credit card required.

---

## Related products by Black Falcon Data

- [StepStone Scraper](https://apify.com/blackfalcondata/stepstone-scraper?fpr=1h3gvi) — Job listings from 18 European portals
- [Indeed Job Scraper](https://apify.com/blackfalcondata/indeed-job-scraper?fpr=1h3gvi) — Indeed job listings with salary data
- [Glassdoor Job Scraper](https://apify.com/blackfalcondata/glassdoor-job-scraper?fpr=1h3gvi) — Glassdoor listings with company ratings
- [Arbeitsagentur Scraper](https://apify.com/blackfalcondata/arbeitsagentur-scraper?fpr=1h3gvi) — Germany's official job portal (1M+ listings)
- [SEEK Scraper](https://apify.com/blackfalcondata/seek-scraper?fpr=1h3gvi) — Australia & NZ's largest job board
- [Naukri Scraper](https://apify.com/blackfalcondata/naukri-scraper?fpr=1h3gvi) — India's largest job portal

---

## Getting started with Apify

New to Apify? [Create a free account with $5 credit](https://console.apify.com/sign-up?fpr=1h3gvi) — no credit card required.

1. Sign up — $5 platform credit included
2. Open [Intermediair Scraper - Dutch professional job board](https://apify.com/blackfalcondata/intermediair-scraper?fpr=1h3gvi) and configure your input
3. Click **Start** — export results as JSON, CSV, or Excel

Need more later? [See Apify pricing](https://apify.com/pricing?fpr=1h3gvi).

---

## About Black Falcon Data

Black Falcon Data builds production-grade web scrapers for job boards and marketplace data. Browse our full actor catalog at [www.blackfalcondata.com](https://www.blackfalcondata.com).

---

*Last updated: 2026 04*
