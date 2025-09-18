# Repository Guidelines

## Project Structure & Module Organization
- `index.html`: Single-page Kabutomushi typing game that renders UI, styles, assets, and gameplay logic inline.
- `search.html`: Lightweight search helper page used for asset/browser experiments.
- `assets/` & `haikei/`: Beetle sprites and background illustrations; keep filenames descriptive and reuse existing dimensions for smooth animation.
- `images/`: Reference mockups and captured screenshots for visual QA; add new evidence here when updating layout.

## Build, Test, and Development Commands
- Run locally without tooling by opening `index.html` in a browser.
- Launch a static server when testing browser security features: `python3 -m http.server 8000` (then visit `http://localhost:8000/index.html`).
- Capture interactive regressions with Playwright: `npx playwright open index.html` for ad‑hoc manual flows or `npx playwright codegen index.html` to script repeatable checks.

## Coding Style & Naming Conventions
- HTML/CSS/JS all live in `index.html`; keep indentation at two spaces and favor multi-line CSS rules for readability.
- Prefer descriptive CSS custom properties (e.g., `--beetle-groundline`) and update related JS helpers when new tokens are introduced.
- JavaScript uses `const`/`let`, arrow functions only where brevity helps, and camelCase identifiers (`spawnBeetle`, `applyModeToUI`).
- Asset filenames should remain lowercase with hyphens or underscores; reuse PNG format to match existing pipeline.

## Testing Guidelines
- No automated unit suite yet; rely on manual smoke tests in both “プログラミング用語” and “UNIXコマンド” modes.
- Before publishing, validate beetle path alignment, word cycling, miss counter, and input focus by launching Playwright (`npx playwright open index.html`) and capturing a screenshot for the `images/` folder when UI changes.
- Document any new manual test scripts or commands in this file to keep future agents aligned.

## Commit & Pull Request Guidelines
- Follow the existing history: concise, imperative subject lines under 60 characters (e.g., `Add mode selector with UNIX command pool`).
- Group related HTML/CSS/JS edits together; avoid unrelated asset churn in the same commit.
- For pull requests, include: summary of user-visible changes, manual test evidence (screenshot link or GIF from `images/`), and mention of any new commands.
- Link to tracking issues when available and call out remaining QA or asset needs so future contributors can pick them up quickly.
