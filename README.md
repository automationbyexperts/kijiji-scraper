# Kijiji.ca Scraper: Canada Cars, Real Estate & Classifieds with Seller Phone Numbers

[![Run on Apify](https://img.shields.io/badge/Apify-Run%20the%20Actor-00A67E?logo=apify&logoColor=white)](https://apify.com/fayoussef/kijiji-scraper?fpr=youssef)
![Seller phone](https://img.shields.io/badge/Seller%20phone-included-2ea44f)
![VIN](https://img.shields.io/badge/VIN-and%20Carfax-1C7ED6)
![GPS](https://img.shields.io/badge/GPS-every%20listing-8B5CF6)
![Export](https://img.shields.io/badge/Export-JSON%20%7C%20CSV%20%7C%20Excel-F59E0B)

> ### ▶️ [Run the Kijiji.ca Scraper on Apify](https://apify.com/fayoussef/kijiji-scraper?fpr=youssef)
> Scrape **Kijiji.ca** cars, apartments for rent, real estate and classifieds with price, **seller phone number**, dealership name, **VIN and Carfax link**, GPS coordinates and photos, from search pages or single ads.

**Kijiji.ca Scraper** turns Kijiji, Canada's largest classifieds site, into clean structured data: 35+ fields per listing from search results (with every page) or direct ad URLs. It is built for car dealers, real estate analysts, landlords and lead generation teams working the Canadian market. This repository documents the Apify Actor and gives working Python, JavaScript and cURL examples for calling it through the API.

- **Run it in the browser:** [fayoussef/kijiji-scraper on Apify](https://apify.com/fayoussef/kijiji-scraper?fpr=youssef)
- **Guide and docs:** [automationbyexperts.com/apify/kijiji-scraper](https://automationbyexperts.com/apify/kijiji-scraper)
- **Actor ID for the API:** `fayoussef/kijiji-scraper`

## What the Kijiji scraper does

- **Any Kijiji category**: cars and trucks, apartments and condos for rent, real estate for sale, jobs and general classifieds.
- **Seller contact data**: `phone_number` and `dealership_name` are resolved per listing, which most Kijiji scrapers skip.
- **Vehicle history**: `vin` and `carfax_link` on car ads.
- **GPS coordinates** on every listing, not just a city name.
- **Search pages and single ads** in one Actor, with automatic pagination.
- **Canadian residential proxies** by default.

## Output fields: what data you get

35+ fields per listing. The main ones:

| Field | Description |
|---|---|
| `id` / `kijiji_url` / `title` / `description` | Ad identity and text |
| `price_amount` / `price_original_amount` / `price_type` | Price and price type |
| `price_classification_rating` | Deal rating on dealer car ads |
| `location_name` / `location_address` / `latitude` / `longitude` | Location and GPS |
| `phone_number` / `dealership_name` / `for_sale_by` | Seller contact, dealer or owner |
| `make` / `model` / `year` / `trim` / `vin` / `mileage_km` | Vehicle details |
| `carfax_link` | Carfax vehicle history URL |
| `transmission` / `fuel_type` / `drivetrain` / `body_type` / `color` | Vehicle specs |
| `features` | A/C, alloy wheels, Bluetooth, sunroof and more |
| `activation_date` / `is_top_ad` | When the ad went live and promotion flags |
| `image_urls` | Photos |

## Input

Set your filters on kijiji.ca, then paste the URL:

| Field | What it does |
|---|---|
| `start_urls` | Kijiji search result URLs or single ad URLs |
| `max_pages` | Result pages per search; leave empty for all |

## Use cases

- **Used car dealers**: monitor dealer and private seller prices across provinces.
- **Lead generation**: build seller call lists with `phone_number` and `dealership_name`.
- **Rental market research**: track apartments for rent by neighbourhood with GPS.
- **Wholesalers**: source vehicles from private sellers.
- **Insurance and finance**: cross-check `vin` and `carfax_link`.

Ready-made examples you can run in one click:

- [Export apartments for rent in Ottawa from Kijiji](https://apify.com/fayoussef/kijiji-scraper/examples/ottawa-apartments-for-rent-kijiji?fpr=youssef): Collects Ottawa apartment and condo rental ads from Kijiji.ca with rent, bedrooms, bathrooms, size, pets, parking, address and photos. Property managers benchmark rents with it; renters use it to see every listing at once.

## Quick start

### 1. In the browser (no code)

1. Search on kijiji.ca with your filters (category, city, price...) and copy the URL.
2. Open the Actor on Apify, click **Try for free** and paste the URL into **Kijiji Search URLs**.
3. Click **Start**, then download Excel, CSV or JSON from the **Output** tab.

### 2. Through the API

1. Create a free [Apify account](https://console.apify.com/sign-up?fpr=youssef) and copy your API token from [Settings > Integrations](https://console.apify.com/settings/integrations).
2. Set it as an environment variable: `export APIFY_TOKEN=...` (PowerShell: `$env:APIFY_TOKEN="..."`).
3. Edit [`input.json`](input.json) and run one of the examples below.

#### Python

```bash
pip install apify-client
python examples/python/run_actor.py
```

```python
import os
from apify_client import ApifyClient

client = ApifyClient(os.environ["APIFY_TOKEN"])
run = client.actor("fayoussef/kijiji-scraper").call(run_input={'start_urls': [{'url': 'https://www.kijiji.ca/b-cars-trucks/calgary/c174l1700199'}],
 'max_pages': 5})

for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

#### JavaScript / Node.js

```bash
npm install apify-client
node examples/javascript/run_actor.mjs
```

```javascript
import { ApifyClient } from "apify-client";

const client = new ApifyClient({ token: process.env.APIFY_TOKEN });
const run = await client.actor("fayoussef/kijiji-scraper").call({
    "start_urls": [
        {
            "url": "https://www.kijiji.ca/b-cars-trucks/calgary/c174l1700199"
        }
    ],
    "max_pages": 5
});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items);
```

#### cURL (plain HTTP)

Runs the Actor and returns the dataset items in one synchronous call:

```bash
curl -X POST "https://api.apify.com/v2/acts/fayoussef~kijiji-scraper/run-sync-get-dataset-items?token=$APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d @input.json
```

Synchronous calls time out after 300 seconds. For larger runs use the client libraries above, or start the run with `POST /v2/acts/fayoussef~kijiji-scraper/runs` and read the dataset when it finishes.

## Sample output

One record, from [`sample-output.json`](sample-output.json). Export the full dataset as JSON, CSV, Excel or HTML from the Apify Console, or read it through the API as shown above.

```json
{
  "id": "m10661116",
  "title": "2024 BMW M4",
  "description": "Presenting the 2024 BMW M4 Competition M xDrive, sold by St. Albert Exotics...",
  "phone_number": "+1-833-870-0000",
  "kijiji_url": "https://kijiji.ca/v-cars-trucks/edmonton/2024-bmw-m4/m10661116",
  "ad_source": "TOP_AD",
  "activation_date": "2025-04-15T23:45:28.000Z",
  "dealership_name": "St. Albert Exotics",
  "location_name": "Edmonton",
  "location_address": "Saint Albert Trail Northwest, Edmonton, AB, T5L 4H5",
  "latitude": 53.5910375,
  "longitude": -113.5649788,
  "price_amount": 99888,
  "price_type": "FIXED",
  "price_surcharges": "PLUS_GST",
  "make": "bmw",
  "model": "m4",
  "year": 2024,
  "mileage_km": 30160,
  "fuel_type": "Gas",
  "drivetrain": "AWD",
  "body_type": "coupe",
  "color": "Black",
  "condition": "Used",
  "for_sale_by": "Dealer",
  "vin": "WBS43AZ04RCP39930",
  "trim": "Competition M xDrive",
  "carfax_link": "https://vhr.carfax.ca/?id=rx6WB4G84rojC55NbLR4s1",
  "seats": 4,
  "doors": 2,
  "features/airconditioning": true,
  "features/sunroof": true,
  "image_urls": [
    "https://media.kijiji.ca/api/v1/autos-prod-ads/images/35/351e0ce4.jpg"
  ],
  "source_search_url": "https://www.kijiji.ca/b-cars-vehicles/edmonton/bmw/k0c27l1700203"
}
```

## Integrations and automation

- **Schedule it** daily to catch new ads as they are posted.
- **Send results** to Google Sheets, Airtable, Slack, a webhook, Make, Zapier or n8n with Apify integrations.
- **Use it from AI agents** through the Apify MCP server.

## FAQ

### Does Kijiji have a public API?
No. This Actor is a Kijiji API alternative: one Apify API call returns structured JSON for every ad.

### Does it return seller phone numbers?
Yes. `phone_number` and `dealership_name` are resolved per listing when Kijiji exposes them.

### Can I scrape apartments for rent on Kijiji?
Yes. Paste a Kijiji rentals search URL, for example apartments for rent in Ottawa or Toronto.

### Can I scrape cars and trucks with VIN?
Yes. Car ads include `vin`, `carfax_link`, make, model, year, mileage and specs.

### How do I filter by price, city or make?
Set the filters on kijiji.ca and paste the resulting URL.

### Can I scrape one ad instead of a search?
Yes. Paste the ad URL directly.

### What output formats are available?
JSON, CSV, Excel, XML and JSONL from the Apify dataset, or through the API.

## Scraper Kijiji en français

Le **Kijiji.ca Scraper** extrait les annonces de Kijiji (autos, appartements à louer, immobilier et petites annonces) avec le prix, le **numéro de téléphone du vendeur**, le concessionnaire, le NIV et le lien Carfax, les coordonnées GPS et les photos. Collez une URL de recherche Kijiji et exportez les résultats en Excel, CSV ou JSON. [Essayer sur Apify](https://apify.com/fayoussef/kijiji-scraper?fpr=youssef).

## Pricing

Pay per use on Apify: you are charged per event (results produced), with no subscription to this Actor. The current rate is shown on the [Actor's Store page](https://apify.com/fayoussef/kijiji-scraper?fpr=youssef). Free-plan runs are capped; an [Apify plan](https://apify.com/pricing?fpr=youssef) unlocks full runs.

## Related scrapers by AutomationByExperts

- [AutoTrader.ca Scraper: Canada Car Listings, VIN & Dealers](https://github.com/automationbyexperts/autotrader-canada-scraper)
- [AutoScout24 Scraper: European Car Listings & Dealer Phones](https://github.com/automationbyexperts/autoscout24-scraper)
- [CarGurus Scraper: US, Canada & UK Car Listings](https://github.com/automationbyexperts/cargurus-scraper)
- [AutoTrader.co.za Scraper: South Africa Cars with Seller Phones](https://github.com/automationbyexperts/autotrader-south-africa-scraper)
- [Bulk AI Image Generator: Nano Banana & GPT Image](https://github.com/automationbyexperts/bulk-ai-image-generator)
- [Bulk LLM Runner: ChatGPT, Claude & Gemini in Bulk](https://github.com/automationbyexperts/bulk-llm-runner)
- [Full catalog of our web scraping APIs](https://github.com/automationbyexperts/web-scraping-apis)

## Support

Questions, bugs or a custom scraper: open an issue here, use the Issues tab on the [Apify page](https://apify.com/fayoussef/kijiji-scraper?fpr=youssef), or email youssefarhan24@gmail.com.

## License

The example code in this repo is MIT licensed. The Actor itself runs on Apify under its own terms.
