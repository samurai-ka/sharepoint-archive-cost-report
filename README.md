# SharePoint Archive Cost Report

A self-contained HTML dashboard for comparing included SharePoint storage, active PAYG storage, and SharePoint Archive storage. The dashboard calculates monthly costs and savings interactively in the browser without external libraries or a backend service.

## Calculation Model

The dashboard uses `1 TB = 1,000 GB` and applies these formulas:

```text
Additional Storage = Total Storage - Included Storage
PAYG Storage = max(0, Additional Storage - Archive Storage)
PAYG Cost = PAYG Storage × 1,000 × PAYG Price
Archive Cost = Billable Archive Storage × 1,000 × Archive Price
Total Cost = PAYG Cost + Archive Cost
Cost Without Archive = Additional Storage × 1,000 × PAYG Price
Savings = Cost Without Archive - Total Cost
Savings Percentage = Savings ÷ Cost Without Archive × 100
Billable Archive Storage = min(Archive Storage, Total Storage - Included Storage)
```

All calculations are performed client-side and update as values change.

## Settings

The **Settings** link in the header opens a panel on the right edge with:

- **Currency**: all currencies offered by the Azure Pricing Calculator (default: Euro). Every amount in the dashboard uses the selected currency. Prices are not converted when the currency changes; enter them in the selected currency.
- **PAYG Price** and **Archive Price** per GB (defaults: 0.20 and 0.05).

The settings are stored in the browser's `localStorage` and restored on the next visit. Invalid stored values fall back to the defaults.

## GitHub Pages

Live dashboard: [https://samurai-ka.github.io/sharepoint-archive-cost-report/](https://samurai-ka.github.io/sharepoint-archive-cost-report/)

## Contributing

Keep changes focused, deterministic, and compatible with the single-file dashboard approach. Do not add secrets, tenant identifiers, tokens, or API keys.

Commit messages must follow [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) and must be written in English. Examples:

```text
feat: add archive cost comparison
fix: allow archive storage slider to reach zero
docs: update GitHub Pages instructions
style: refine dashboard colors
```

Before submitting a change, verify the dashboard in a browser and confirm that storage limits, automatic corrections, cost formulas, and responsive layout still work as expected.

## Disclaimer

Taxes, rounding differences, contractual terms, and other cost components are not included. All information is provided without warranty.
