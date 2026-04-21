# sindre-ai.github.io

Landing page for [sindre.ai](https://sindre.ai) — the website for **Maskin**, an open-source workspace for teams working with AI agents.

## About

This repository hosts the static single-page site served at [sindre.ai](https://sindre.ai) via GitHub Pages. The Maskin product itself lives in a separate repository: [github.com/sindre-ai/maskin](https://github.com/sindre-ai/maskin).

## Contents

- `index.html` — the full single-page site (HTML, CSS, and JS inlined)
- `CNAME` — custom domain configuration (`sindre.ai`) for GitHub Pages
- `README.md` — this file

## Local development

There is no build step. To preview changes locally, either open `index.html` directly in a browser, or serve the directory:

```sh
python3 -m http.server 8000
```

Then visit [http://localhost:8000](http://localhost:8000).

## Deployment

Pushes to the default branch are published automatically by GitHub Pages. The `CNAME` file wires the site to the `sindre.ai` domain.

## Links

- Website: [sindre.ai](https://sindre.ai)
- Product repository: [github.com/sindre-ai/maskin](https://github.com/sindre-ai/maskin)
