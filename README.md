# LeaseRadar

A self-contained, mobile-first lease research dashboard built for one person. It keeps the numbers, shortlist, and saved offers in one quiet workspace without adding accounts, subscriptions, or product infrastructure.

Open `index.html` in any modern browser. There is no build process and there are no dependencies.

## Features

- Vehicle shortlist and persistent watchlist
- Search and towing-candidate filters
- Saved advertised offers, estimates and written dealer quotes
- Effective monthly cost calculator and comparison table
- JSON export/import for backups
- Dealer-inventory web search links (not verified inventory)

## Important limitations

This is an offline-first MVP, **not a live-data service**. Vehicle specs and tow capability must be verified by trim and VIN. It does not currently fetch offers, monitor price changes, notify users, sync devices, or connect to dealer inventory feeds. Saved data is browser-local; back it up using the export button.

## Use

1. Open `index.html`.
2. Add vehicles to the watchlist and enter advertised offers or dealer quotes.
3. Use the calculator and comparison table to compare true effective monthly costs.
4. Export a JSON backup before changing browsers or devices.

## Optional deployment

The current app is a static file and can be hosted on any static provider. Live alerts or automated deal collection would require a small backend, scheduled checks, approved data sources, storage, and an email service. Those are future personal-tool enhancements, not prerequisites for using this version.

## Calculator convention

The total due at signing **includes the first monthly payment**. Effective cost = ((term - 1) × monthly payment + due at signing - refundable deposit) / term. Taxes and fees are only accounted for if entered in the payment/DAS figures.

## Privacy

All watchlist and offer data stays in the current browser's local storage unless it is exported manually. The app contains no analytics, authentication, or remote data sync.
