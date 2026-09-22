# SharePoint Archive Cost Report

A self-contained HTML dashboard for comparing included SharePoint storage, active PAYG storage, and SharePoint Archive storage. The dashboard calculates monthly costs and savings interactively in the browser without external libraries or a backend service.

## Features

- Fluent UI-inspired responsive dashboard layout
- Interactive storage sliders and numeric inputs
- Storage allocation bar with Included, PAYG, and Archive segments
- Monthly cost summary and live calculation formulas
- Read-only pricing fields with an explicit Edit/Done workflow
- Escape key support to cancel price edits and restore the previous value
- Defensive validation for negative, empty, oversized, and invalid values
- GitHub Pages-compatible single-file deployment

## Project Structure

```text
.
├── index.html
├── README.md
└── .github/
    ├── copilot-instructions.md
    └── instructions/
        ├── code-quality.instructions.md
        └── reporting-domain.instructions.md
```

## Running Locally

No build step or package installation is required. Open [index.html](index.html) directly from the filesystem in a modern browser.

## Inputs and Limits

| Input | Default | Unit | Limit |
| --- | ---: | --- | ---: |
| Included Storage | 5 | TB | 0-1,000 TB |
| Total Storage | 15 | TB | 0-2,000 TB |
| Archive Storage | 3 | TB | 0-Total Storage |
| PAYG Price | 0.20 | EUR/GB | 0-5 EUR/GB |
| Archive Price | 0.05 | EUR/GB | 0-5 EUR/GB |

Storage values use whole numbers. Price values support two decimal places. If Total Storage is below Included Storage, Total Storage is increased to match Included Storage. Archive Storage can include data within the included quota, but only the archive portion above the included quota is billable.

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

All calculations are performed client-side and update as values change. Archive cost is calculated from `min(Archive Storage, Total Storage - Included Storage)` so archived data within the licensed quota does not create an additional archive charge.

The model follows the Microsoft 365 Archive pricing conditions described in the [Microsoft Learn pricing model](https://learn.microsoft.com/en-us/microsoft-365/archive/archive-pricing?view=o365-worldwide): storage is charged only when combined active and archived storage exceeds the tenant's included or licensed SharePoint capacity. It does not model reactivation charges because Microsoft eliminated that fee on March 31, 2025. The service and billing subscription must remain available for new archive actions; those operational states are outside this cost estimate.

## Visual Conventions

- Included Storage: SharePoint blue `#0078d4`
- PAYG allocation within Total Storage: Red10 `#d13438`
- Archive Storage: YellowGreen10 `#8cbd18`
- Savings Percentage: Green20 `#0b6a0b`
- Storage allocation bar: maximum width `500px`, responsive on smaller screens

## GitHub Pages

The dashboard is already suitable for GitHub Pages because it is a standalone HTML file.

Live dashboard: [https://samurai-ka.github.io/sharepoint-archive-cost-report/](https://samurai-ka.github.io/sharepoint-archive-cost-report/)

1. Push the repository to GitHub.
2. Open **Settings > Pages** for the repository.
3. Select **Deploy from a branch**.
4. Select the branch and the repository root as the folder.
5. Save the configuration and wait for the Pages deployment.

The generated Pages URL will be shown in the repository's Pages settings.

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
