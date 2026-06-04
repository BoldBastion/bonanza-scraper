[Bonanza Scraper](https://apify.com/lulzasaur/bonanza-scraper?fpr=data)

# Bonanza Scraper

Apify Actor for scraping Bonanza marketplace listings by keyword. Uses CheerioCrawler for fast, efficient HTML parsing without a browser.

## Features

- Search Bonanza marketplace by keyword
- Two modes: quick search results or full detail scraping
- Extracts prices with shipping costs from structured HTML markup
- Detail mode captures: full description, all images, seller info, item traits (condition, brand, model, category), and availability
- Handles pagination automatically (60 items per page)
- Identifies featured/promoted listings and top-rated sellers

## Input

| Field | Type | Default | Description |
| --- | --- | --- | --- |
| `searchQueries` | string[] | `["vintage watch"]` | Search terms to scrape |
| `maxListings` | integer | `100` | Max listings per query (0=unlimited) |
| `scrapeDetails` | boolean | `false` | Visit each listing for full details |
| `proxyConfiguration` | object | `{}` | Proxy settings (optional for Bonanza) |

### Example Input

```
{
    "searchQueries": ["vintage watch", "leather bag"],
    "maxListings": 50,
    "scrapeDetails": true
}
```

## Output

### Search-only mode (`scrapeDetails: false`)

```
{
    "title": "Vintage Hamilton Quartz LCD Watch 14K Electroplated",
    "price": 59.99,
    "currency": "USD",
    "shipping": "$5.99 ship",
    "freeShipping": false,
    "imageUrl": "https://images-bucket.bonanzastatic.com/afu/images/.../s-l960.jpg",
    "thumbnailUrl": "https://images-bucket.bonanzastatic.com/afu/images/.../s-l960_thumb200.jpg",
    "url": "https://www.bonanza.com/listings/Vintage-Hamilton-Watch/1777932987",
    "itemId": "1777932987",
    "position": 1,
    "isFeatured": false,
    "hasVariations": false,
    "isTopSeller": true,
    "searchQuery": "vintage watch",
    "scrapedAt": "2026-03-17T12:00:00.000Z"
}
```

### Detail mode (`scrapeDetails: true`)

```
{
    "title": "Vintage Hamilton Quartz LCD Watch 14K Electroplated",
    "price": 59.99,
    "currency": "USD",
    "description": "Great condition vintage Hamilton watch...",
    "fullDescription": "Full seller-provided description text...",
    "images": [
        "https://images-bucket.bonanzastatic.com/afu/images/.../s-l960.jpg"
    ],
    "imageCount": 5,
    "condition": "Used",
    "conditionSchema": "Used",
    "category": "Wristwatches",
    "fullCategory": "Jewelry & Watches/Watches/Wristwatches",
    "brand": "Hamilton",
    "model": "Quartz LCD",
    "quantityAvailable": "Only one in stock, order soon",
    "availability": "Limited",
    "traits": {
        "Category": "Wristwatches",
        "Condition": "Used",
        "Brand": "Hamilton",
        "Model": "Quartz LCD"
    },
    "sellerName": "retrosupplyco",
    "sellerBoothId": "retrosupplyco",
    "sellerBoothUrl": "https://www.bonanza.com/booths/retrosupplyco",
    "isFeatured": false,
    "searchQuery": "vintage watch",
    "scrapedAt": "2026-03-17T12:00:00.000Z"
}
```

## How It Works

1. Builds search URLs for each query using Bonanza's Rails-style query params (`q[search_term]`)
2. Parses search results from server-rendered HTML (`div.search_result_item`)
3. Extracts prices from structured spans (`.money-whole`, `.money-decimal`)
4. Handles pagination via `q[page]` parameter (60 items per page, up to 34+ pages)
5. Optionally visits each listing detail page for rich data extraction
6. Detail pages are parsed via meta tags, schema.org markup, and HTML trait tables

## Quick Start

```
$apify run --purge
```

## Deploy to Apify

```
apify login
apify push
```

## Related Scrapers

More marketplace scrapers and data tools by [lulzasaur](https://apify.com/lulzasaur):

- [AbeBooks Scraper](https://apify.com/lulzasaur/abebooks-scraper) — Rare and used books
- [Contractor License Verifier](https://apify.com/lulzasaur/contractor-license-scraper) — Multi-state license verification
- [Craigslist Scraper](https://apify.com/lulzasaur/craigslist-scraper) — Classifieds and for-sale posts
- [Goodreads Scraper](https://apify.com/lulzasaur/goodreads-scraper) — Book ratings and reviews
- [Grailed Scraper](https://apify.com/lulzasaur/grailed-scraper) — Luxury fashion resale
- [Houzz Scraper](https://apify.com/lulzasaur/houzz-scraper) — Home improvement professionals
- [IMDb Scraper](https://apify.com/lulzasaur/imdb-scraper) — Movie and TV show data
- [Nurse License Verifier](https://apify.com/lulzasaur/nurse-license-scraper) — State nursing board verification
- [OfferUp Scraper](https://apify.com/lulzasaur/offerup-scraper) — Local marketplace listings
- [Poshmark Scraper](https://apify.com/lulzasaur/poshmark-scraper) — Fashion resale marketplace
- [PSA Population Report](https://apify.com/lulzasaur/psa-pop-scraper) — Card grading data
- [Redfin Scraper](https://apify.com/lulzasaur/redfin-scraper) — Real estate listings and prices
- [Reverb Scraper](https://apify.com/lulzasaur/reverb-scraper) — Music gear marketplace
- [StubHub Scraper](https://apify.com/lulzasaur/stubhub-scraper) — Event ticket prices
- [Swappa Scraper](https://apify.com/lulzasaur/swappa-scraper) — Used electronics marketplace
- [TCGPlayer Scraper](https://apify.com/lulzasaur/tcgplayer-scraper) — Trading card prices
- [ThriftBooks Scraper](https://apify.com/lulzasaur/thriftbooks-scraper) — Used book prices
- [Thumbtack Scraper](https://apify.com/lulzasaur/thumbtack-scraper) — Local service professionals