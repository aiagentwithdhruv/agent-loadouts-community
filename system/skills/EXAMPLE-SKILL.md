# Skill: web-scraper

> Scrape structured data from any website using configurable extractors, with anti-detection, rate limiting, and output validation.

---

## Trigger

Use this skill when:
- User asks to scrape data from a website
- User says "extract", "pull data from", "crawl", or "harvest" from a web page
- User needs structured data (names, prices, emails, reviews) from a URL
- User wants to monitor a website for changes

Do NOT use this skill when:
- Target is Google Maps specifically (use `gmaps-leads` instead)
- Target requires login/authentication (use `ghost-browser` instead)
- User wants to scrape social media feeds (use platform-specific skills)
- The data is available via a public API (use the API directly)

---

## Prerequisites

### Tools & Runtime
| Tool | Version | Install |
|------|---------|---------|
| Python | 3.10+ | `brew install python3` |
| playwright | latest | `pip install playwright && playwright install chromium` |
| beautifulsoup4 | latest | `pip install beautifulsoup4` |
| pandas | latest | `pip install pandas` |

### Credentials
| Name | Where to Get It | Store In |
|------|----------------|----------|
| `PROXY_URL` | Any rotating proxy provider (optional but recommended) | `.env` |

No API keys required for basic scraping. Proxy is optional but strongly recommended for large-scale jobs or sites with rate limiting.

### Files Required
| File | Purpose |
|------|---------|
| `scripts/scrape.py` | Main scraper with configurable extractors |
| `scripts/validate.py` | Output validation and deduplication |
| `templates/selectors.json` | Pre-built CSS selector configs for common sites |

### Pre-Checks
Before running, verify:
1. Target URL is accessible: `curl -s -o /dev/null -w "%{http_code}" {url}` (expect 200)
2. Playwright is installed: `python3 -c "from playwright.sync_api import sync_playwright; print('OK')"`
3. Output directory exists: `mkdir -p output/`

---

## Execution

### Step 1: Analyze the Target Page
Open the target URL and identify the data structure:
```bash
python3 scripts/scrape.py --analyze --url "https://example.com/products"
```
**Expected result:** Prints detected data patterns (lists, tables, cards) and suggested CSS selectors.
**If it fails:** The page may require JavaScript rendering. Add `--render` flag to use Playwright instead of raw HTTP.

### Step 2: Configure Extractors
Create or select a selector config:
```bash
# Use a pre-built config
python3 scripts/scrape.py --url "https://example.com/products" \
  --config templates/selectors.json \
  --preset ecommerce

# OR define custom selectors inline
python3 scripts/scrape.py --url "https://example.com/products" \
  --selectors '{
    "name": "h2.product-title",
    "price": "span.price",
    "rating": "div.stars @data-rating",
    "url": "a.product-link @href"
  }'
```
**Expected result:** Extraction config is validated and ready.
**If it fails:** Check CSS selectors in browser DevTools. Selector syntax: `tag.class` for text, `tag @attr` for attributes.

### Step 3: Run the Scraper
```bash
python3 scripts/scrape.py --url "https://example.com/products" \
  --config templates/selectors.json \
  --preset ecommerce \
  --pages 5 \
  --delay 2 \
  --output output/raw_data.csv
```
**Expected result:** Scrapes up to 5 pages with 2-second delays between requests. Saves raw data to CSV.
**If it fails:**
- `403 Forbidden` -- Add `--proxy $PROXY_URL` or `--rotate-ua` for random User-Agent headers
- `Timeout` -- Increase with `--timeout 30`
- `Captcha detected` -- Reduce speed with `--delay 5` or use proxy

### Step 4: Validate and Clean Output
```bash
python3 scripts/validate.py \
  --input output/raw_data.csv \
  --rules '{"name": "required|min:2", "price": "required|numeric", "url": "required|url"}' \
  --output output/clean_data.csv
```
**Expected result:** Removes duplicates, validates fields, outputs clean CSV with stats.

### Step 5: Review Results
```bash
python3 -c "
import pandas as pd
df = pd.read_csv('output/clean_data.csv')
print(f'Total rows: {len(df)}')
print(f'Columns: {list(df.columns)}')
print(df.head())
print(f'\nNull counts:\n{df.isnull().sum()}')
"
```
**Expected result:** Summary of scraped data with row counts and completeness check.

---

## Output

### Deliverables
| Deliverable | Format | Location |
|-------------|--------|----------|
| Raw scraped data | CSV | `output/raw_data.csv` |
| Cleaned/validated data | CSV | `output/clean_data.csv` |
| Scrape log | JSON | `output/scrape_log.json` |

### Quality Criteria
- All required fields populated (no nulls in required columns)
- No duplicate rows (deduplicated on primary key)
- URLs are absolute (not relative paths)
- Numeric fields parse correctly (prices as floats, ratings as integers)
- Encoding is UTF-8 (no garbled characters)

### Sample Output
```csv
name,price,rating,url,scraped_at
"Wireless Bluetooth Headphones",49.99,4.5,"https://example.com/products/headphones-123","2026-03-01T10:30:00Z"
"USB-C Charging Cable 6ft",12.99,4.2,"https://example.com/products/cable-456","2026-03-01T10:30:01Z"
"Laptop Stand Adjustable",34.99,4.7,"https://example.com/products/stand-789","2026-03-01T10:30:02Z"
```

---

## Schema

### Inputs
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `url` | string | Yes | -- | Target URL to scrape |
| `selectors` | object | Yes* | -- | CSS selector map (key: field name, value: selector) |
| `config` | file_path | Yes* | -- | Path to selector config file (*either selectors or config required) |
| `preset` | string | No | -- | Pre-built selector set (ecommerce, directory, reviews, jobs) |
| `pages` | integer | No | 1 | Number of pages to scrape (follows pagination) |
| `delay` | float | No | 1.0 | Seconds between requests |
| `render` | boolean | No | false | Use Playwright for JavaScript-rendered pages |
| `proxy` | string | No | -- | Proxy URL for anti-detection |
| `max_results` | integer | No | 500 | Maximum rows to return |
| `validation_rules` | object | No | -- | Field validation rules for cleaning |

### Outputs
| Name | Type | Description |
|------|------|-------------|
| `raw_csv` | file_path | Path to raw scraped data |
| `clean_csv` | file_path | Path to validated/cleaned data |
| `row_count` | integer | Number of rows in clean output |
| `scrape_log` | file_path | Path to JSON log with timing, errors, stats |
| `success_rate` | float | Percentage of pages successfully scraped |

### Credentials
| Name | Source | Required |
|------|--------|----------|
| `PROXY_URL` | .env | No (recommended for production) |

### Composable With

| Direction | Skill | How |
|-----------|-------|-----|
| **Output to** | `classify-leads` | Feed clean_csv as input for lead scoring |
| **Output to** | `casualize-names` | Feed name column for formatting |
| **Output to** | `instantly-campaigns` | Feed email column for outreach |
| **Output to** | `create-proposal` | Use scraped company data in proposals |
| **Input from** | `cross-niche-outliers` | Scrape URLs found during research |

### Cost
| Component | Cost |
|-----------|------|
| Scraping (no proxy) | Free |
| Proxy (if used) | ~$1-5 per 1000 requests |
| Playwright rendering | Free (local compute) |
| **Total per run** | **$0 - $5 typical** |

---

## Error Handling

| Error | Cause | Fix |
|-------|-------|-----|
| `403 Forbidden` | Site blocks the request | Add `--rotate-ua` and/or `--proxy`. If persistent, increase `--delay` to 5+ seconds |
| `Timeout after 10s` | Page takes too long to load | Increase `--timeout 30`. Check if site is down: `curl -I {url}` |
| `Captcha detected` | Anti-bot triggered | Reduce request rate (`--delay 10`), use residential proxy, or try at off-peak hours |
| `Selector not found` | CSS selector doesn't match page structure | Open URL in browser, inspect element, update selector. Page may have changed layout |
| `0 results on page 2+` | Pagination pattern changed | Check pagination URL format. May need `--pagination-selector "a.next-page"` |
| `UnicodeDecodeError` | Non-UTF-8 encoding | Add `--encoding latin-1` or let the scraper auto-detect with `--encoding auto` |
| `Empty CSV output` | No elements matched selectors | Run `--analyze` again. Site may have restructured. Check for iframe-embedded content |

### Common Mistakes
| Mistake | Why It Happens | Prevention |
|---------|---------------|------------|
| Scraping too fast | Default delay too low for target | Always start with `--delay 2` minimum. Increase for sensitive sites |
| Using static HTTP on JS-heavy sites | Data is rendered client-side | Check page source vs rendered page. If different, use `--render` |
| Hardcoding selectors for dynamic sites | Class names change (e.g., Tailwind hashes) | Use data attributes (`[data-testid="price"]`) or structural selectors (`div > span:nth-child(2)`) |
| Not validating output | Garbage data passes through | Always run `validate.py` after scraping |
| Ignoring robots.txt | Legal/ethical risk | Check `{domain}/robots.txt` first. Respect disallow rules |

### Retry Logic
- **Transient failures** (timeout, 429, 503): Retry up to 3 times with exponential backoff (2s, 4s, 8s)
- **Permanent failures** (404, 401): Do not retry. Log and skip.
- **Partial results**: Save what was collected. Report which pages failed. Resume with `--start-page N`.

---

## Templates

### Preset: ecommerce
```json
{
  "name": "ecommerce",
  "selectors": {
    "product_name": "h2.product-title, h3.product-name, [data-testid='product-title']",
    "price": "span.price, .product-price, [data-testid='price']",
    "original_price": "span.original-price, .was-price, s .price",
    "rating": "div.stars @data-rating, span.rating, [itemprop='ratingValue']",
    "review_count": "span.review-count, .num-reviews",
    "image_url": "img.product-image @src, .product-img img @src",
    "product_url": "a.product-link @href, h2 a @href"
  },
  "pagination": "a.next-page @href, [aria-label='Next'] @href"
}
```

### Preset: directory
```json
{
  "name": "directory",
  "selectors": {
    "business_name": "h2.listing-name, .business-name, [itemprop='name']",
    "address": ".listing-address, [itemprop='streetAddress']",
    "phone": ".listing-phone, [itemprop='telephone']",
    "website": "a.website-link @href",
    "category": ".listing-category, .business-type",
    "description": ".listing-description, [itemprop='description']"
  },
  "pagination": "a.next @href, .pagination li.next a @href"
}
```

### Preset: reviews
```json
{
  "name": "reviews",
  "selectors": {
    "reviewer": ".review-author, [itemprop='author']",
    "rating": ".review-rating @data-rating, [itemprop='ratingValue']",
    "date": ".review-date, [itemprop='datePublished']",
    "title": ".review-title, h3.review-heading",
    "body": ".review-text, [itemprop='reviewBody']",
    "verified": ".verified-purchase"
  },
  "pagination": "a[aria-label='Next page'] @href"
}
```

---

## Examples

### Example 1: Scrape Product Listings

**Scenario:** Extract all products from an e-commerce category page.

**Input:**
```json
{
  "url": "https://example-store.com/electronics/headphones",
  "preset": "ecommerce",
  "pages": 3,
  "delay": 2,
  "render": false
}
```

**Command:**
```bash
python3 scripts/scrape.py \
  --url "https://example-store.com/electronics/headphones" \
  --config templates/selectors.json \
  --preset ecommerce \
  --pages 3 \
  --delay 2 \
  --output output/raw_data.csv

python3 scripts/validate.py \
  --input output/raw_data.csv \
  --rules '{"product_name": "required", "price": "required|numeric|min:0.01"}' \
  --output output/clean_data.csv
```

**Output:**
```
Scraping page 1/3... 24 items found
Scraping page 2/3... 24 items found
Scraping page 3/3... 18 items found
Total: 66 raw rows saved to output/raw_data.csv

Validating...
Removed 2 duplicates
Removed 1 row (missing price)
Clean: 63 rows saved to output/clean_data.csv
```

### Example 2: Scrape a JavaScript-Heavy SPA

**Scenario:** Extract job listings from a React-based job board.

**Input:**
```json
{
  "url": "https://jobs.example.com/search?q=python+developer&loc=remote",
  "selectors": {
    "title": "[data-testid='job-title']",
    "company": "[data-testid='company-name']",
    "salary": "[data-testid='salary-range']",
    "location": "[data-testid='job-location']",
    "posted": "[data-testid='date-posted']",
    "url": "[data-testid='job-title'] a @href"
  },
  "pages": 5,
  "delay": 3,
  "render": true,
  "max_results": 200
}
```

**Command:**
```bash
python3 scripts/scrape.py \
  --url "https://jobs.example.com/search?q=python+developer&loc=remote" \
  --selectors '{"title":"[data-testid=\"job-title\"]","company":"[data-testid=\"company-name\"]","salary":"[data-testid=\"salary-range\"]","location":"[data-testid=\"job-location\"]","posted":"[data-testid=\"date-posted\"]","url":"[data-testid=\"job-title\"] a @href"}' \
  --pages 5 \
  --delay 3 \
  --render \
  --max-results 200 \
  --output output/raw_data.csv
```

**Output:**
```
Launching Playwright (headless Chromium)...
Scraping page 1/5... 20 items found (rendered in 2.3s)
Scraping page 2/5... 20 items found (rendered in 1.8s)
Scraping page 3/5... 20 items found (rendered in 2.1s)
Scraping page 4/5... 20 items found (rendered in 1.9s)
Scraping page 5/5... 15 items found (rendered in 2.0s)
Total: 95 raw rows saved to output/raw_data.csv
```

### Example 3: Chain with Lead Enrichment

**Scenario:** Scrape a business directory, then classify and format leads for outreach.

```bash
# Step 1: Scrape the directory
python3 scripts/scrape.py \
  --url "https://directory.example.com/dentists/austin-tx" \
  --config templates/selectors.json \
  --preset directory \
  --pages 10 \
  --output output/raw_leads.csv

# Step 2: Classify leads (using classify-leads skill)
python3 ../classify-leads/scripts/classify.py \
  --input output/raw_leads.csv \
  --criteria "dental practice, 4+ rating, has website" \
  --output output/scored_leads.csv

# Step 3: Format names (using casualize-names skill)
python3 ../casualize-names/scripts/casualize.py \
  --input output/scored_leads.csv \
  --column business_name \
  --output output/ready_leads.csv
```

This is the **lead-enrichment chain** in action: `web-scraper -> classify-leads -> casualize-names`.

---

## Self-Update Rules

### After Every Run
1. If a new error type is encountered, add to the Error Handling table
2. If a new site pattern is scraped successfully, consider adding a preset to Templates
3. If output quality drops below 80% valid rows, investigate selector accuracy

### After Site Changes
1. If a commonly-scraped site changes its layout, update the relevant preset
2. If anti-bot measures increase, document the new bypass in Error Handling
3. If new anti-detection techniques work, add to the Execution steps

### After Composition
1. If this skill is used in a new chain, add the skill to Composable With
2. If a downstream skill needs a new output field, add it to the Schema

### Cross-File Updates
When updating this file, also check:
- `../../LOADOUT.md` -- version, changelog
- `../../.claude/CLAUDE.md` -- if triggers changed
- `../INDEX.md` -- if name or description changed

---

## Changelog

| Date | Change | By |
|------|--------|-----|
| 2026-03-01 | Initial skill creation with 3 presets (ecommerce, directory, reviews) | AiwithDhruv |
