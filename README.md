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
| Archive Storage | 3 | TB | 0-available additional storage |
| PAYG Price | 0.20 | EUR/GB | 0-5 EUR/GB |
| Archive Price | 0.05 | EUR/GB | 0-5 EUR/GB |

Storage values use whole numbers. Price values support two decimal places. If Total Storage is below Included Storage, Total Storage is increased to match Included Storage. Archive Storage is reduced automatically when it exceeds the available additional storage.

## Calculation Model

The dashboard uses `1 TB = 1,000 GB` and applies these formulas:

```text
Additional Storage = Total Storage - Included Storage
PAYG Storage = Additional Storage - Archive Storage
PAYG Cost = PAYG Storage × 1,000 × PAYG Price
Archive Cost = Archive Storage × 1,000 × Archive Price
Total Cost = PAYG Cost + Archive Cost
Cost Without Archive = Additional Storage × 1,000 × PAYG Price
Savings = Cost Without Archive - Total Cost
Savings Percentage = Savings ÷ Cost Without Archive × 100
```

All calculations are performed client-side and update as values change.

## Visual Conventions

- Included Storage: SharePoint blue `#0078d4`
- PAYG allocation within Total Storage: Red10 `#d13438`
- Archive Storage: YellowGreen10 `#8cbd18`
- Savings Percentage: Green20 `#0b6a0b`
- Storage allocation bar: maximum width `500px`, responsive on smaller screens

## GitHub Pages

The dashboard is already suitable for GitHub Pages because it is a standalone HTML file.

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
