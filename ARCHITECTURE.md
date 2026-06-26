# Architecture

## High-Level Flow

```text
Search keyword + region
        |
        v
Playwright browser session
        |
        v
Google Maps search and result scrolling
        |
        v
Captured list/detail HTML
        |
        v
BeautifulSoup parser and deterministic fallbacks
        |
        v
Normalized business records
        |
        +--> Optional local Ollama JSON cleanup
        |
        +--> Optional website enrichment
        |
        v
CSV / JSON output
```

## Main Components

### Browser Automation

The browser layer opens Google Maps, submits a search query, waits for the results feed, scrolls the result list, detects when the list reaches the end, and captures the loaded HTML for parsing.

### Listing Parser

The parser extracts structured fields from listing cards and detail views. It handles multiple fallback patterns because Google Maps markup can vary between list cards, detail panels, localizations, and business categories.

Important parser behavior includes:

- Rating and review extraction from visible text and aria labels
- Phone number extraction and cleanup
- Address and business-hours separation
- Category and location inference from listing text blocks
- Detail-page fallback parsing when card data is incomplete

### Local LLM Cleanup

The local LLM step uses Ollama to convert raw listing snippets into strict JSON records. It is intentionally optional: deterministic parsing remains available when the LLM service is not running or when the response cannot be decoded as JSON.

### Website Enrichment

The enrichment step can visit business websites found in Google Maps listings. It reads homepage/about/contact-style pages and extracts public signals such as email addresses, social links, service labels, team/about text, and useful page metadata.

### Output Layer

The output layer writes normalized records to CSV and JSON. This keeps the workflow simple for portfolio use, manual review, later database import, or CRM lead enrichment.

## Data Shape

Typical normalized record:

```json
{
  "name": "Example Business",
  "rating": "4.7",
  "reviews": "120",
  "category": "Service category",
  "location": "City or address",
  "hours": "Open - Closes 6PM",
  "phone": "123-456-7890",
  "website": "https://example.com"
}
```

## Extension Points

The system can be extended with:

- PostgreSQL storage
- Deduplication by phone, website, or business name
- CRM import jobs
- Lead scoring by rating, review volume, category, and website quality
- Scheduled research runs
- Dashboard review workflow
- Portfolio assistant retrieval from sanitized project docs

