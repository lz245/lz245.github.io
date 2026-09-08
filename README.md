# Zhang Lab Website

Source for **https://lz245.github.io** — the Zhang Lab (Agricultural
Microbiomes & Food Safety, Department of Poultry Science, Mississippi State
University).

Built with [Quarto](https://quarto.org). Served free by GitHub Pages from the
`docs/` folder on `main`.

---

## How publishing works (read this first)

**Editing content does not require Quarto, git, or a terminal.** Change a file
on github.com and click *Commit changes*; a GitHub Actions workflow
(`.github/workflows/publish.yml`) renders the site, commits the rebuilt `docs/`
folder, and asks GitHub Pages to publish it. The change is live in roughly two
to four minutes.

**If you are not a developer, stop here and read
[guide/how-to-update-the-website.md](guide/how-to-update-the-website.md)** — a plain-English
guide to adding news posts, lab members, publications, and photos through the
browser.

If a build fails, the previously published site keeps serving; nothing goes
down. Failures appear as a red X under the repository's **Actions** tab.

### Working locally (optional)

Only needed for design or structural work. Requires the
[Quarto CLI](https://quarto.org/docs/get-started/) — this site is built with
Quarto **1.10.18**, pinned to the same version in the workflow so local and CI
output match. No R or Python needed.

```
quarto preview         # live preview while editing
quarto render          # writes the site into docs/
```

You may commit `docs/` along with your source changes, but you no longer need
to — pushing source alone is enough, and the workflow will rebuild and commit
`docs/` for you.

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

Each page of the site is one `.qmd` file at the top level. Quarto turns
`people.qmd` into `/people.html`, so these stay at the root — moving them into
a subfolder would change every page's web address and break existing links.

```
index.qmd              the pages of the site, one file each
people.qmd             (people.qmd -> /people.html, and so on)
research.qmd
publications.qmd
teaching.qmd
join.qmd
404.qmd

news/                  news posts (one .qmd per post)
protocols/             protocol pages (linked from the navbar)
data/people/           lab-member data (one YAML per role group)
assets/images/         images (run scripts/optimize-images.ps1 after adding)
assets/fonts/          self-hosted WOFF2 fonts
styles/custom.scss     the entire design system
guide/                 plain-English guide for non-technical maintainers
scripts/               maintenance scripts

_quarto.yml            site config (nav, profiles, theme)
_quarto-prod.yml       production profile (GA, robots)
_quarto-preview.yml    preview profile (noindex)
_partials/             footer + site JS (injected every page)
_templates/            EJS templates for generated grids (people)
.github/workflows/     automatic build-and-publish
docs/                  RENDERED OUTPUT — never edit by hand
```

Config files (`_quarto*.yml`, `.nojekyll`) must stay at the repository root;
Quarto and GitHub Pages look for them there.

## Adding a custom domain later

The site currently publishes at `lz245.github.io`. If a custom domain is ever
added through **Settings → Pages**, GitHub writes a `CNAME` file into the
published folder — and `quarto render` will delete it on the next build. To
make it survive, put a `CNAME` file containing the bare domain at the
repository root and register it in `_quarto.yml`:

```yaml
project:
  resources:
    - CNAME
```

Then update `site-url:` in `_quarto.yml` to the new domain.
