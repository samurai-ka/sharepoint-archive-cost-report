---
applyTo: "**/*.{html,js,md,sql,json,yml,yaml}"
---

# Reporting domain guidance

This project is about SharePoint archive storage and cost reporting. When generating or changing report logic:

- Understand whether values are stored, calculated, or aggregated before rendering.
- Keep units and date ranges explicit in output and documentation.
- Favor transparent calculations over hidden assumptions.
- Check for missing data, empty ranges, and ambiguous month boundaries.
- Ensure output remains useful for finance and operational reviews.

## Storage and cost model

- Included Storage default: 1 TB
- Total Storage default: 1 TB
- Archive Storage default: 0 TB
- Currency default: EUR (selectable in the Settings panel from the Azure Pricing Calculator currencies; no conversion)
- PAYG Price default: €0.20/GB
- Archive Price default: €0.05/GB
- Currency, PAYG Price and Archive Price are persisted in localStorage
- 1 TB = 1000 GB

## Business rules

- Additional Storage = Total Storage - Included Storage
- Archive Storage cannot exceed Additional Storage
- PAYG Storage = Additional Storage - Archive Storage
- If Total Storage is less than Included Storage, raise the value to Included Storage and show a validation message
- If Archive Storage exceeds available Additional Storage, reduce it automatically and show a validation message
- Negative values and values above 10,000 TB must be rejected or clamped safely

## Cost formulas

- PAYG Cost = PAYG Storage × 1000 × PAYG Price
- Archive Cost = Archive Storage × 1000 × Archive Price
- Total Cost = PAYG Cost + Archive Cost
- Cost Without Archive = Additional Storage × 1000 × PAYG Price
- Savings = Cost Without Archive - Total Cost
- Savings Percentage = Savings ÷ Cost Without Archive × 100

## Dashboard output expectations

- Show KPI cards for Total Storage, PAYG Storage, Archive Storage, and Monthly Savings
- Use Fluent UI-inspired card treatments, balanced spacing, and clear hierarchy across all summary blocks
- Display a live formula like: 15 TB total − 5 TB included − 3 TB archive = 7 TB PAYG
- Show cost summary with Active PAYG Storage Cost, Archive Storage Cost, Total Cost, Cost Without Archive, Savings, and Savings Percentage
- Show legend entries with current TB and current cost for archive and PAYG storage, plus included storage TB
- Include footer text: "Disclaimer: Taxes, rounding differences, contractual terms and other cost components are not included. All information is provided without warranty."
