# Kijiji.ca Scraper: Autos, Real Estate & Classifieds

Efficiently scrapes Kijiji.ca listings: vehicles, real estate, and more. Extracts detailed data including phone number, price, location, specs, and images from search results (with pagination) or direct ad URLs. Ideal for market research and data collection.

This repo shows how to call the [Kijiji.ca Scraper: Autos, Real Estate & Classifieds](https://apify.com/fayoussef/kijiji-scraper?fpr=youssef) Apify Actor from your own code: a Python and a JavaScript example, the input they send, and a sample of the output. Everything runs in the Apify cloud, so there is nothing to host, scale or maintain on your side.

- **Run it in the browser:** [fayoussef/kijiji-scraper on Apify](https://apify.com/fayoussef/kijiji-scraper?fpr=youssef)
- **Guide and docs:** [automationbyexperts.com/apify/kijiji-scraper](https://automationbyexperts.com/apify/kijiji-scraper)
- **Actor ID for the API:** `fayoussef/kijiji-scraper`

## Use cases

- [Scrape used cars and trucks in Calgary on Kijiji](https://apify.com/fayoussef/kijiji-scraper/examples/calgary-used-trucks-kijiji?fpr=youssef): Reads the Calgary cars and trucks category on Kijiji.ca and returns each ad with price, year, make, model, kilometres, drivetrain, dealer or private flag, location and photos. Alberta's private truck market, refreshed on whatever schedule you set.
- [Export apartments for rent in Ottawa from Kijiji](https://apify.com/fayoussef/kijiji-scraper/examples/ottawa-apartments-for-rent-kijiji?fpr=youssef): Collects Ottawa apartment and condo rental ads from Kijiji.ca with rent, bedrooms, bathrooms, size, pets, parking, address and photos. Property managers benchmark rents with it; renters use it to see every listing at once.

## Quick start

1. Create a free [Apify account](https://console.apify.com/sign-up?fpr=youssef) and copy your API token from [Settings > Integrations](https://console.apify.com/settings/integrations).
2. Set it as an environment variable: `export APIFY_TOKEN=...` (PowerShell: `$env:APIFY_TOKEN="..."`).
3. Edit [`input.json`](input.json) and run one of the examples below.

### Python

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

### JavaScript / Node.js

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

### cURL (plain HTTP)

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

## Pricing

Pay per use on Apify: you are charged per event (results produced), with no subscription to this Actor. The current rate is shown on the [Actor's Store page](https://apify.com/fayoussef/kijiji-scraper?fpr=youssef). Free-plan runs are capped; an [Apify plan](https://apify.com/pricing?fpr=youssef) unlocks full runs.

## More Actors by AutomationByExperts

- [AutoTrader Canada Car Scraper: Prices, VIN, Mileage & Dealers](https://github.com/automationbyexperts/autotrader-canada-scraper)
- [AutoScout24 All-Country Scraper](https://github.com/automationbyexperts/autoscout24-scraper)
- [CarGurus Scraper (US, Canada & UK Car Listings)](https://github.com/automationbyexperts/cargurus-scraper)
- [autotrader.co.za Car Scraper with Seller Phone Numbers](https://github.com/automationbyexperts/autotrader-south-africa-scraper)
- [Bulk AI Image Generator (NO API KEY)](https://github.com/automationbyexperts/bulk-ai-image-generator)
- [Bulk LLM Runner GPT, Claude, Perplexity, Kimi (No API Key)](https://github.com/automationbyexperts/bulk-llm-runner)
- [Full catalog of our web scraping APIs](https://github.com/automationbyexperts/web-scraping-apis)

## Support

Questions, bugs or a custom scraper: open an issue here, use the Issues tab on the [Apify page](https://apify.com/fayoussef/kijiji-scraper?fpr=youssef), or email youssefarhan24@gmail.com.

## License

The example code in this repo is MIT licensed. The Actor itself runs on Apify under its own terms.
