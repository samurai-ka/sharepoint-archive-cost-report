# GitHub Copilot instructions for sharepoint-archive-cost-report

## Project goal
This repository supports a SharePoint archive cost report and related dashboarding. Keep changes focused on clarity, reproducibility, cost transparency, and a professional dashboard experience for SharePoint storage planning.

## Working principles
- Prefer small, reviewable changes over broad refactors.
- Keep scripts and reports deterministic and easy to rerun.
- Document assumptions, especially around dates, storage calculations, and cost logic.
- Favor explicit data handling for missing, empty, unexpected, or invalid values.
- Avoid hardcoded tenant-specific values when configuration is possible.
- Keep all calculations client-side and transparent when delivering HTML-based reports and dashboards.

## Dashboard and implementation standards
- Build self-contained dashboards using only HTML, CSS, and vanilla JavaScript.
- Keep the entire dashboard in a single HTML file unless a separate asset is explicitly required.
- Use a responsive Fluent UI-inspired design with card-based layout, clear spacing, subtle shadows, and modern Microsoft design language.
- Use Fluent UI color tokens and visual patterns such as soft borders, segmented surfaces, and consistent elevation.
- Keep all labels and content in English.
- Use accessible form controls, synchronized sliders and number inputs, and clear validation messaging.
- Do not use external libraries or frameworks unless explicitly required for Fluent UI styling; the default expectation remains lightweight vanilla HTML/CSS/JS.
- Use strict mode, addEventListener-based interactions, and modular functions with clear variable names.

## Business logic requirements
- Compare Included Storage, Active PAYG Storage, and SharePoint Archive Storage.
- Use 1 TB = 1024 GB for all calculations.
- Additional Storage = Total Storage - Included Storage.
- Archive Storage cannot exceed Additional Storage.
- PAYG Storage = Additional Storage - Archive Storage.
- If Total Storage is smaller than Included Storage, automatically increase Total Storage and show a validation message.
- If Archive Storage exceeds available Additional Storage, automatically reduce Archive Storage and show a validation message.
- Validate negative values, zero values, large values above 10,000 TB, and invalid ranges without JavaScript errors.

## Cost and reporting rules
- PAYG Cost = PAYG Storage × 1024 × PAYG Price
- Archive Cost = Archive Storage × 1024 × Archive Price
- Total Cost = PAYG Cost + Archive Cost
- Cost Without Archive = Additional Storage × 1024 × PAYG Price
- Savings = Cost Without Archive - Total Cost
- Savings Percentage = Savings ÷ Cost Without Archive × 100
- Keep units, totals, and formulas clearly visible in the dashboard output.

## UI expectations
- Show top KPI cards for Total Storage, PAYG Storage, Archive Storage, and Monthly Savings.
- Create a single large vertical stacked bar with Included Storage at the bottom, PAYG in the middle, and Archive on top.
- Use color coding: green for Included, Microsoft blue for PAYG, purple for Archive.
- Display labels inside each segment, along with a legend showing current TB and cost values.
- Include a yearly cost summary (monthly costs × 12), a live formula section, and a footer disclaimer.

## Coding and reporting standards
- Use descriptive names for files, variables, and report fields.
- Keep transformations simple and easy to validate.
- Preserve clear output naming and consistent units for storage and cost.
- Add comments only where they clarify non-obvious logic or business rules.
- Validate with the smallest relevant test or execution path when changing logic.

## Data and security
- Never commit secrets, tokens, API keys, or tenant identifiers in source files.
- Treat report data as sensitive and avoid exposing internal details in logs or sample output.
- Keep validation and cleanup logic explicit so data quality issues are visible.

## Documentation expectations
- Update the project documentation when behavior, inputs, or outputs change.
- Explain any operational assumptions in a way that a teammate can understand quickly.
- Prefer concise, practical notes over verbose prose.

## Review checklist before completion
- Does the change improve the visibility or accuracy of archive cost reporting?
- Is the result understandable to another maintainer?
- Are edge cases handled without surprising behavior?
- Is the dashboard aligned with the requested storage and cost logic?
- Is the documentation still aligned with the implementation?
