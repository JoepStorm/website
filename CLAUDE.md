# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A fork of the **Academic Pages** Jekyll template (itself derived from Minimal Mistakes), used as a personal academic website hosted on GitHub Pages. The template is intentionally kept close to upstream so it can be synced/rebased; avoid sweeping refactors that would create merge conflicts with `academicpages/academicpages.github.io`.

## Common commands

Local preview (Jekyll, served at `localhost:4000`, live-reloads on Markdown/HTML changes but **not** `_config.yml`):
```bash
bundle install
bundle exec jekyll serve -l -H localhost
```

Docker alternative (uses `_config_docker.yml`):
```bash
docker compose up
```

JS bundle (concatenates jQuery, fitvids, smooth-scroll, plotly, plugins, and `_main.js` into `assets/js/main.min.js`):
```bash
npm run build:js          # one-shot
npm run watch:js          # rebuild on change
```

Regenerate `_data/cv.json` from `_pages/cv.md`:
```bash
./scripts/update_cv_json.sh
```

Generate publication / talk markdown files from TSV/CSV/BibTeX in `markdown_generator/`:
```bash
cd markdown_generator
python3 publications.py    # reads publications.tsv, writes to ../_publications/
python3 talks.py           # reads talks.tsv, writes to ../_talks/
python3 pubsFromBib.py     # build pubs from a .bib file
```

## Architecture

### Content lives in collections, not pages
Each "thing" (publication, talk, post, portfolio item, teaching entry) is a single Markdown file with YAML front matter inside its `_<collection>/` directory. The collections are configured in `_config.yml` under `collections:` and rendered through layouts in `_layouts/` (e.g. `single.html`, `archive.html`, `talk.html`). To add content, drop a new `.md` file in the right `_<collection>/` folder — do **not** edit a generated index page.

`_pages/` holds the standalone pages (about, CV, publications index, etc.) that are not part of a collection.

### Layout / include / sass cascade
- `_layouts/` — page skeletons; most content layouts extend `default.html`.
- `_includes/` — partials pulled into layouts (`head/`, `footer/`, `analytics-providers/`, `comments-providers/`, `toc/`, `nav_list`, etc.). Provider folders use the value set in `_config.yml` (e.g. `comments.provider`) to pick the right partial.
- `_sass/` — SCSS partials compiled by `assets/css/main.scss`. Theming is driven by `site_theme` in `_config.yml` (`default`, `air`, `sunrise`, `mint`, `dirt`, `contrast`); each maps to a `_sass/_themes/` file.

### Site-wide config
`_config.yml` is the single source of truth for site identity, author sidebar links, analytics/comments providers, collections, and defaults. Jekyll does **not** auto-reload it — restart `jekyll serve` after edits. `_config_docker.yml` is the Docker-specific override.

### Data files
`_data/` drives content that needs structured access:
- `navigation.yml` — top nav menu.
- `authors.yml` — multi-author overrides for posts.
- `cv.json` — generated from `_pages/cv.md` by `scripts/cv_markdown_to_json.py`; consumed by `_includes/cv-template.html`. Treat `cv.json` as a build artifact — edit `cv.md` and rerun the script.
- `ui-text.yml` — i18n strings keyed by `locale` in `_config.yml`.

### Generators vs. hand-edited content
`markdown_generator/` (Python scripts and Jupyter notebooks) produces files in `_publications/` and `_talks/` from tabular sources. If a publication file already exists and you regenerate, it will be overwritten — so either edit the TSV/CSV/bib source and regenerate, or stop using the generator for that entry. `talkmap.ipynb` (and the GitHub Action `scrape_talks.yml`) geocodes talk locations and writes `talkmap.html`; it runs automatically on push to `_talks/**` or `talks/**`.

### Hosting
The site is deployed by GitHub Pages' built-in Jekyll build (no custom build action). The only workflow in `.github/workflows/` is `scrape_talks.yml`, which commits `talkmap_out.ipynb` back to the repo. `_site/` is the local build output and should not be committed.
