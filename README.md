# Alex Motyka Engineering Portfolio

MkDocs Material site for resume and engineering case studies.

## Local setup

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
mkdocs serve
```

Open the local URL printed by MkDocs.

## Build

```bash
mkdocs build --strict
```

## Deploy

Push to `main`. The GitHub Actions workflow in `.github/workflows/pages.yml` builds the site and deploys it to GitHub Pages.

In GitHub repository settings, set Pages source to **GitHub Actions**.
