---
applyTo: "**/*.{html,css,js,ts,py,md,json,yml,yaml}"
---

# Code quality and front-end constraints

- Use HTML, CSS, and vanilla JavaScript only.
- Keep the dashboard self-contained in one file when possible.
- Use strict mode and modular functions with clear, descriptive names.
- Prefer explicit validation over implicit behavior.
- Use addEventListener() for all interactions instead of inline event handlers.
- Do not use eval() or other unsafe runtime evaluation.
- Keep the style aligned with Fluent UI principles: soft surfaces, clear hierarchy, neutral backgrounds, subtle borders, and accessible color contrast.
- Use Fluent-inspired spacing and typography rather than older Microsoft-style heavy chrome.
- Ensure no JavaScript errors can occur during normal interaction.
- Handle negative, zero, empty, and oversized values defensively.
- Keep responsive layouts, accessible labels, and consistent naming across inputs and outputs.
- Make debugging easy by keeping logic readable and scoped to the task.
