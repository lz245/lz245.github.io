# Zhang Lab Website

Source for **https://lz245.github.io** — the Zhang Lab (Agricultural
Microbiomes & Food Safety, Department of Poultry Science, Mississippi State
University).

Built with [Quarto](https://quarto.org). Served free by GitHub Pages from the
`docs/` folder on `main`.

---

## How publishing works (read this first)

> **Transitioning to automatic publishing.** A GitHub Actions workflow
> (`.github/workflows/publish.yml`) renders and deploys the site on every push
> to `main`. It becomes active once the repository setting
> **Settings → Pages → Source** is changed to **GitHub Actions**.
>
> - **Before that switch:** follow the manual steps below — render locally and
>   commit `docs/` — or the live site will not update.
> - **After that switch:** just edit source and push. No local render, no
>   `docs/` commit. Rendering happens on GitHub, and a stalled build reports
>   itself as a failed run instead of silently serving a stale site.

GitHub Pages currently serves whatever is in **`main:/docs`**. Until the
setting above is switched, nothing deploys automatically from source files —
you must render locally and commit the result:

```
# 1. edit source files (.qmd, data/, styles/)
quarto render          # writes the site into docs/
git add -A
git commit -m "Describe your change"
git push
```

Live in ~1–3 minutes. If you push source changes **without** rendering,
the live site does not change.

Requirements: [Quarto CLI](https://quarto.org/docs/get-started/) (this site
was built with Quarto **1.10**; use 1.10+ so rendered output stays
consistent). No R or Python needed.

Preview while editing: `quarto preview`

---

## Everyday edits

### Add a news post

Create `news/YYYY-MM-DD-short-slug.qmd`:

```markdown
---
title: "Sunita wins a travel award"
date: 2026-09-15
description: >
  One or two sentences shown in news listings and on the homepage.
categories: [Awards]        # Awards | Publications | Media | Announcements
---

Body of the post in plain Markdown.
```

The News page and the homepage "Latest updates" strip pick it up
automatically on the next render.

### Add or update a lab member

People cards are generated from YAML files in `data/people/` —
`faculty.yml`, `staff.yml`, `postdocs.yml`, `phd.yml`, `ms.yml`,
`undergrad.yml`. Add a block:

```yaml
- name: Jane Doe
  role: Ph.D. Student, Poultry Science
  photo: assets/images/team/jane-doe.jpg   # optional; card shows initials without it
  blurb: One or two sentences about their research.
  award: Optional award line
  email: jd123@msstate.edu
  scholar: https://scholar.google.com/...   # optional
```

Drop the photo (any size) into `assets/images/team/`, then run the image
pipeline once so the site never ships huge camera files:

```
powershell -ExecutionPolicy Bypass -File scripts\optimize-images.ps1
```

Alumni are edited directly in `people.qmd` (the "Alumni" section).

### Add a publication

Edit `publications.qmd` — add a numbered entry at the top of the right year
section, following the existing format (bold **Zhang, L.**, `\*` marks
corresponding author, DOI link at the end). Update the count in the
`.pub-stats` block if it crosses a threshold.

### Add a protocol

Copy `protocols/_template.qmd` to `protocols/short-name.qmd` and fill in the
standard sections (Materials, Equipment, Safety, Procedure, Troubleshooting).
Set `title`, `description`, `date`, and `categories` in the front matter —
the Lab Protocols table picks it up automatically. Photos go in
`assets/images/` (run the image pipeline after adding).

---

## Design system

All styling lives in `styles/custom.scss` (tokens at the top: MSU maroon
`#660000`, gold `#d4a017`, warm paper ground). Fonts are self-hosted in
`assets/fonts/` (Fraunces / Archivo / Source Sans 3) — no external font
requests. The site footer is `_partials/site-tail.html`, injected on every
page; lab contact details live there and only there.

Accessibility: color pairs are WCAG AA; all motion respects
`prefers-reduced-motion`; every image needs alt text.

## Build profiles

- `quarto render` — **production** (default): indexable, Google Analytics on.
- Preview builds (for staging on a fork):
  `$env:QUARTO_PROFILE="preview"; quarto render` — adds `noindex`, no
  analytics.

## Repo layout

```
_quarto.yml            site config (nav, profiles, theme)
_quarto-prod.yml       production profile (GA, robots)
_quarto-preview.yml    preview profile (noindex)
_partials/             footer + site JS (injected every page)
_templates/            EJS templates for generated grids (people)
data/people/           lab-member data (one YAML per role group)
news/                  news posts (one .qmd per post)
protocols/             protocol pages (hidden from nav until populated)
assets/images/         images (run scripts/optimize-images.ps1 after adding)
assets/fonts/          self-hosted WOFF2 fonts
styles/custom.scss     the entire design system
scripts/               maintenance scripts
docs/                  RENDERED OUTPUT — never edit by hand
```
