# GameVault & StyleHub Scraping 

Datasets produced by two web scrapers built for FAST-NUCES Data Science Assignment 1 (Web Scraping): a static scraper for GameVault's full product catalog, and a dynamic (Selenium/Playwright) scraper for StyleHub's infinite-scroll landing page prototype.

## Files

| File | Description |
|---|---|
| `23L_1008_versionA_static_products.csv` | 3,000 products scraped from [sandbox.oxylabs.io/products](https://sandbox.oxylabs.io/products) across 94 paginated listing pages, merged with per-product detail-page data (stock status, description). |
| `23L_1008_versionA_dynamic_products.csv` | 147 unique products scraped from [scrapingcourse.com/infinite-scrolling](https://www.scrapingcourse.com/infinite-scrolling) via Selenium-driven scrolling, merged with detail-page data (SKU, short description). |
| `23L_1008.ipynb` | Jupyter notebook containing both scrapers, a Playwright bonus implementation, and methodology write-up. |

## Static Dataset — Columns
`name`, `price`, `stock_status`, `description`, `detail_url`, `listing_page`

## Dynamic Dataset — Columns
`name`, `price`, `image_url`, `scroll_batch`, `sku`, `short_description`, `detail_url`, `loaded_via_scroll`

## Methodology (brief)

- **Static scraper**: `requests` + `BeautifulSoup`, with a persistent `requests.Session()`, self-terminating pagination (stops using the site's own reported result total, not a hardcoded page count), and retry-with-backoff on detail-page fetches.
- **Dynamic scraper**: Selenium with explicit waits (`WebDriverWait`) on DOM element count rather than fixed sleeps; deduplicated by detail URL to handle repeated elements during scroll re-rendering; batch number records when each product first appeared.
- Full methodology, validation statistics, and a Selenium vs. Playwright comparison are documented in the notebook.


