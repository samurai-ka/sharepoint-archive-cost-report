# Notes for Claude

Project-internal reminders that don't belong in README.md (end-user/contributor docs). Check this
file at the start of a session in this repo.

## Pending: switch GitHub Pages source when `feature/pnp-integration` merges to `main`

The `feature/pnp-integration` branch moved the dashboard (`index.html`, `manifest.json`, `icons/`)
into `src/` and added [.github/workflows/pages.yml](.github/workflows/pages.yml) to publish `src/`
via GitHub's Actions-based Pages deployment.

**Do not switch the Pages source before this branch is merged into `main`.** As of the last check,
this repo's Pages source is still the legacy "Deploy from a branch" mode (`main`, root `/`), which
is what currently serves the live dashboard correctly — because `main` still has `index.html` at
its root. Switching to "GitHub Actions" now, before `src/` exists on `main`, would break the live
site immediately (no successful Actions deployment would exist yet).

**When this branch (or its restructuring) is merged into `main`:**

1. Remind the user this step is due, unless they've already asked for it in the same request.
2. If asked to proceed, switch the Pages source using the `gh` CLI (already authenticated as the
   repo owner in this environment):
   ```
   gh api repos/samurai-ka/sharepoint-archive-cost-report/pages -X PUT -f build_type=workflow
   ```
3. Verify: `gh api repos/samurai-ka/sharepoint-archive-cost-report/pages` should report
   `"build_type":"workflow"`. Then trigger or wait for the `pages.yml` workflow run and confirm it
   succeeds (`gh run list --workflow=pages.yml`), and that the live URL still serves the dashboard.
4. Once confirmed working, this note can be removed from this file.
