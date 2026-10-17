# LeaseRadar

A single-user dashboard for live dealer inventory, current manufacturer lease programs, watched vehicles, effective lease costs, and saved dealer quotes.

The public site is hosted on GitHub Pages at [hamrick.github.io/leaseradar](https://hamrick.github.io/leaseradar/). It contains no authentication, analytics, or multi-user product infrastructure.

## What works

- Dealer inventory near ZIP code `78641`, filtered to the configured vehicle shortlist
- Current OEM lease programs for watched makes and models
- Distance, price, color, and tow-candidate filters
- VIN watchlist stored in the browser
- Scheduled refresh every six hours
- GitHub Issue alerts for newly seen matching VINs and lease programs
- Effective-payment calculator
- Saved quote comparison and JSON backup/restore

Inventory and incentive data comes from the MarketCheck APIs. LeaseRadar keeps the API key in GitHub Actions secrets and publishes only the normalized results used by the dashboard.

## One-time live-data setup

1. Create a MarketCheck API key at [developers.marketcheck.com](https://developers.marketcheck.com/).
2. In this repository, open **Settings → Secrets and variables → Actions**.
3. Add a repository secret named `MARKETCHECK_API_KEY`.
4. Open **Actions → Refresh LeaseRadar data → Run workflow**.
5. Watch this repository's Issues if you want GitHub to notify you about newly found matches.

Until the secret is configured, the site shows an explicit setup state. It never presents demo records as live data.

## Search and alert rules

Edit [`config/searches.json`](config/searches.json) to change ZIP code, radius, watched models, trim notes, color requirements, and tow-candidate flags. The scheduled workflow reads that file on every run.

## How the refresh works

The workflow in [`.github/workflows/refresh-data.yml`](.github/workflows/refresh-data.yml):

1. Searches MarketCheck's active new-car inventory for each configured model.
2. Retrieves current OEM lease programs for the watched makes near the configured ZIP code.
3. Normalizes results into `data/inventory.json` and `data/incentives.json`.
4. Opens a GitHub issue when a later refresh discovers a new matching VIN or program.
5. Commits changed data so GitHub Pages publishes the new results.

The first successful refresh establishes a baseline and does not create a flood of alert issues.

## Accuracy and privacy

- Inventory and offers can change between refreshes. Always verify price, availability, equipment, towing capacity, eligibility, taxes, fees, and lease terms with the dealer or lessor.
- MarketCheck supplies inventory and manufacturer programs; it does not guarantee a vehicle-specific lease quote.
- Saved dealer quotes and watched VINs stay in the current browser's local storage unless manually exported.
- GitHub Issue alerts and the normalized feed are public because this repository and its Pages site are public. The API key remains private.

## Local use

Serve the repository with any static web server. Opening `index.html` directly may prevent JSON loading in some browsers.

```sh
python3 -m http.server 4173
```

Then visit `http://localhost:4173`.
