# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Joel Fiddes' professional CV system. Deployed as a GitHub Pages site at https://joelfiddes.github.io/cv/ with auto-generated PDFs in three formats.

## File Structure

- `index.md` — Primary CV source (Markdown with embedded HTML links)
- `cv-screen.css` — Screen stylesheet (MF brand colors)
- `cv-print.css` — Print/PDF stylesheet (loaded last to override screen styles)
- `cv-adb.html` — ADB TECH-5 format CV (standalone HTML, edit directly)
- `cv-europass.html` — Europass format CV (standalone HTML, edit directly)
- `cv.html` — Local preview (in .gitignore, generated manually)
- `mf_logo.png` — Mountain Futures logo (shown on web, hidden in print)
- `signature.png` — Joel's signature for ADB certification section
- `.github/workflows/deploy.yml` — CI: builds HTML from markdown, generates PDFs, deploys

## Build & Deploy

Pushes to `main` trigger the GitHub Action which:
1. Converts `index.md` → `index.html` via pandoc
2. Builds a separate `cv-main-print.html` (no download button, print CSS last)
3. Generates PDFs with Chromium headless (`google-chrome --headless --print-to-pdf`)
4. Deploys everything to GitHub Pages

**Local preview**: `pandoc index.md --from markdown --to html --no-highlight` and wrap in the HTML template (see `cv.html` or the workflow for the template).

**PDF generation** uses Chromium headless (not weasyprint — weasyprint chokes on CSS shorthand). The print HTML loads `cv-screen.css` first, then `cv-print.css` so print styles win.

## Conventions for index.md

- Date labels: backtick-wrapped ranges (`` `2022-present` ``)
- Institutions: `__bold__`
- Roles: `_italic_`
- Links: HTML `<a href="...">` tags (not Markdown `[]()` syntax)
- Author name in publications: `**Fiddes, J.**` or `**Joel Fiddes**`
- Update the "Last updated" date at the bottom when making changes

## Brand Colors (Mountain Futures)

- Forest green: `#639033` (download button, h2 in screen)
- Sky blue/teal: `#91ccd9` (h2, h3, subtitle, date labels, links in print)
- Dark grey: `#4b4b4b` (h1)
- Date labels: `#858585` (screen), `#91ccd9` (print)

## CSS Notes

- Logo (`mf_logo.png`) displayed via `#main::before` pseudo-element in screen CSS
- Logo and download button hidden in print via `@media print` and `cv-print.css`
- **Avoid** CSS `font:` shorthand — weasyprint and some tools can't parse it. Use explicit `font-style`, `font-weight`, `font-family` etc.
- When editing print styles, remember print CSS loads after screen CSS so it overrides. Any screen reset (e.g., `list-style: none`) must be explicitly re-set in print CSS.

## ADB CV (`cv-adb.html`)

The ADB CV is a standalone HTML file in TECH-5 table format. Edit it directly.

### How to update for a new proposal

1. **Section 1 (Proposed Position)** — Update the position title per the TOR
2. **Section 2 (Name of Firm)** — Update to the bidding firm (e.g., Landell Mills Ltd, Mountain Futures GmbH)
3. **Section 4 (DOB/Citizenship)** — DOB is 31/10/1981. Citizenship: adjust per proposal (British, or British / Swiss)
4. **Section 9 (Countries)** — Add/remove countries relevant to the assignment
5. **Section 12 (Detailed Tasks)** — Replace with tasks from the TOR. Include the specialist profile/requirements paragraph at the top, then list tasks grouped by theme
6. **Section 13 (Project Experience)** — Reorder project entries to best match the TOR. Put the most relevant projects first. Add/remove entries as needed
7. **Section 14 (Certification)** — Signature image (`signature.png`) is embedded. Update the date

### Current project entries in section 13
- RBWRP (Balochistan, Landell Mills/EU)
- SDC SAPPHIRE / SnowMapper
- CROMO-ADAPT & WWCS
- UNESCO/GEF Climate Scenarios
- WMO Cryosphere Monitoring
- FutureWater Bhagirathi Basin
- World Bank Tajikistan Disaster Assessment

### Placeholder fields
Red placeholder text uses class `placeholder`. Remove these before submission. The CSS style can be kept for future template use.

## Europass CV (`cv-europass.html`)

Standalone HTML with inline CSS. Blue themed (`#1e5a96`). Edit directly. Sections: header, work experience, education, personal skills (CEFR language table), publications, memberships, grants.

## Gotchas

- The `.gitignore` excludes `*.pdf` and `cv.html` — PDFs are generated in CI only
- `index_main.html` in the repo root is a leftover and can be deleted
- Google Fonts (Open Sans) are loaded from CDN in the web version — won't render in offline/print; the print CSS falls back to system sans-serif
- Font Awesome icons in `#webaddress` require the CDN link in the HTML template
