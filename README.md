# SharePoint Archive Cost Report

A self-contained HTML dashboard for comparing included SharePoint storage, active PAYG storage, and SharePoint Archive storage. The dashboard calculates monthly costs and savings interactively in the browser without external libraries or a backend service.

## Calculation Model

The dashboard uses `1 TB = 1,024 GB` and applies these formulas:

```text
Additional Storage = Total Storage - Included Storage
PAYG Storage = max(0, Additional Storage - Archive Storage)
PAYG Cost = PAYG Storage × 1,024 × PAYG Price
Archive Cost = Billable Archive Storage × 1,024 × Archive Price
Total Cost = PAYG Cost + Archive Cost
Cost Without Archive = Additional Storage × 1,024 × PAYG Price
Savings = Cost Without Archive - Total Cost
Savings Percentage = Savings ÷ Cost Without Archive × 100
Billable Archive Storage = min(Archive Storage, Total Storage - Included Storage)
Yearly Cost = Monthly Cost × 12
```

The KPI cards and the Storage Allocation card show monthly costs. The Yearly Cost Summary projects the current monthly costs (including Savings) over 12 months and assumes that the storage values stay constant.

All calculations are performed client-side and update as values change.

## Settings

The **Settings** link in the header opens a panel on the right edge with:

- **Currency**: all currencies offered by the Azure Pricing Calculator (default: Euro). Every amount in the dashboard uses the selected currency. Prices are not converted when the currency changes; enter them in the selected currency.
- **PAYG Price** and **Archive Price** per GB (defaults: 0.20 and 0.05).

The settings are stored in the browser's `localStorage` and restored on the next visit. Invalid stored values fall back to the defaults.

## Installing as an app

The page ships a [web app manifest](src/manifest.json) and icons (`src/icons/`), so Edge or Chrome can install it as a standalone app: open the site, then use the browser menu → **Apps** → **Install this site as an app**. The app icon is the "Money" glyph from the [Fluent UI System Icons](https://github.com/microsoft/fluentui-system-icons) library on a Fluent-blue background.

## GitHub Pages

Live dashboard: [https://samurai-ka.github.io/sharepoint-archive-cost-report/](https://samurai-ka.github.io/sharepoint-archive-cost-report/)

[.github/workflows/pages.yml](.github/workflows/pages.yml) publishes `src/` to GitHub Pages on every
push to `main` that touches `src/`, using GitHub's Actions-based Pages deployment
(`actions/configure-pages`, `actions/upload-pages-artifact`, `actions/deploy-pages`). It can also be
run manually from the Actions tab.

**One-time setup** (repository admin, once): under **Settings → Pages**, set **Source** to
**GitHub Actions**. Before this switch, Pages is served directly from the branch root, which no
longer matches this layout now that the dashboard lives under `src/`.

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
