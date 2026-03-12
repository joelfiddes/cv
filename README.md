# Joel Fiddes — CV

Professional CV deployed at **https://joelfiddes.github.io/cv/**

## Formats

| Format | Description |
|--------|-------------|
| [Web CV](https://joelfiddes.github.io/cv/) | Main CV with download button |
| [PDF](https://joelfiddes.github.io/cv/cv-main.pdf) | Print-optimised PDF |
| [ADB TECH-5](https://joelfiddes.github.io/cv/cv-adb.pdf) | Asian Development Bank format |
| [Europass](https://joelfiddes.github.io/cv/cv-europass.pdf) | EU Europass format |

## How it works

- `index.md` is the source CV in Markdown
- On push to `main`, a GitHub Action builds the HTML (via pandoc), generates PDFs (via Chromium headless), and deploys to GitHub Pages
- ADB and Europass CVs are standalone HTML files edited directly

## Local preview

```bash
BODY=$(pandoc index.md --from markdown --to html --no-highlight)
# Wrap in template — see .github/workflows/deploy.yml or cv.html
```

## Branding

[Mountain Futures GmbH](https://mountainfutures.ch) — science-based consulting on mountain water resources, cryosphere monitoring, and climate risk.
