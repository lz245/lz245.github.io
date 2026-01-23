# Zhang Lab Website

[![Website](https://img.shields.io/badge/website-live-brightgreen)](https://lz245.github.io)
[![Quarto](https://img.shields.io/badge/built%20with-Quarto-blue)](https://quarto.org)

Professional academic research lab website for the **Zhang Lab** at Mississippi State University, Department of Poultry Science. Built with [Quarto](https://quarto.org) and hosted on GitHub Pages.

**Research Focus:** Agricultural microbiomes, pathogen genomics, vaccine development, rapid diagnostics

---

## 📋 Table of Contents

- [Site Structure](#-site-structure)
- [File Reference](#-file-reference)
- [Quick Start](#-quick-start)
- [Common Tasks](#-common-tasks)
- [Deployment](#-deployment)
- [Versioning & Releases](#-versioning--releases)
- [Troubleshooting](#-troubleshooting)
- [Resources](#-resources)

---

## 📁 Site Structure

```
lz245.github.io/
│
├── 📄 CONTENT FILES (edit these regularly)
│   ├── index.qmd                # Homepage - news, highlights, intro
│   ├── research.qmd             # Research programs and projects
│   ├── publications.qmd         # Publication list by year
│   ├── team.qmd                 # Lab members and alumni
│   ├── teaching.qmd             # Courses and student awards
│   └── join.qmd                 # Prospective students/postdocs
│
├── 📊 DATA FILES (structured data)
│   ├── _data/
│   │   └── team.yml             # Team member data (optional, for R-based team page)
│   └── publications.bib         # BibTeX bibliography (optional)
│
├── 🎨 STYLING & CONFIG
│   ├── _quarto.yml              # ⭐ Main site configuration
│   ├── styles/
│   │   ├── custom.scss          # Colors, fonts, custom CSS
│   │   ├── custom.css           # Additional CSS overrides
│   │   └── apa-cv.csl           # Citation format style
│   └── CNAME                    # Custom domain (if using)
│
├── 📸 ASSETS
│   └── assets/
│       └── images/
│           ├── team/            # Member photos (300x300px recommended)
│           ├── lab-logo.png     # Lab logo
│           └── ...              # Other images
│
├── ⚙️ BUILD & DEPLOY
│   ├── .github/
│   │   └── workflows/
│   │       └── publish.yml      # GitHub Actions auto-deploy
│   ├── .gitignore               # Files to exclude from git
│   └── README.md                # This file
│
└── 📦 OUTPUT (auto-generated, do not edit)
    ├── docs/                   # Rendered website files
    ├── _freeze/                 # Quarto computation cache
    └── .quarto/                 # Quarto cache
```

---

## 📖 File Reference

### Content Pages

| File | Purpose | Update Frequency |
|------|---------|------------------|
| `index.qmd` | Homepage with lab intro, news, featured publications | Monthly (news updates) |
| `research.qmd` | Research programs and active projects | Annually or when grants change |
| `publications.qmd` | Complete publication list by year | When papers are published |
| `team.qmd` | Current members, alumni, lab photos | When team changes |
| `teaching.qmd` | Courses, student awards | Each semester |
| `join.qmd` | Open positions, application info | When positions open/close |

### Configuration Files

| File | Purpose | When to Edit |
|------|---------|--------------|
| `_quarto.yml` | Site title, navigation, URL, analytics | Initial setup, rarely after |
| `styles/custom.scss` | Colors, fonts, spacing | To change visual theme |
| `CNAME` | Custom domain name | If using custom domain |

### Data Files

| File | Purpose | Format |
|------|---------|--------|
| `_data/team.yml` | Structured team data (optional) | YAML |
| `publications.bib` | Bibliography for R-based pub page | BibTeX |

---

## 🚀 Quick Start

### Prerequisites

- [Quarto](https://quarto.org/docs/get-started/) (1.4+)
- [Git](https://git-scm.com/)
- Text editor (VS Code, RStudio, or any editor)

> **Note:** R is NOT required for the current setup. The site uses static Markdown pages.

### Local Development

```bash
# Clone the repository
git clone https://github.com/lz245/lz245.github.io.git
cd lz245.github.io

# Preview locally (opens browser with live reload)
quarto preview

# Render the site (generates docs/ folder)
quarto render
```

### Making Changes

```bash
# 1. Edit files (e.g., add a publication)
#    Open publications.qmd and add entry

# 2. Preview changes
quarto preview

# 3. Commit and push
git add .
git commit -m "Add 2025 publication: Jia et al. pagP vaccine"
git push origin main

# 4. GitHub Actions auto-deploys (wait ~2 minutes)
```

---

## 🔄 Common Tasks

### Adding a New Publication

1. Open `publications.qmd`
2. Add entry under the appropriate year section:
   ```markdown
   ## 2025
   
   1. **Zhang, L.**, Author, B., & Author, C. (2025). Paper title here. 
      *Journal Name*, 10(2), 123-456. [DOI](https://doi.org/10.xxxx/xxxxx)
   ```
3. Commit: `git commit -m "Add publication: Author et al. 2025"`

### Adding a New Team Member

1. Open `team.qmd`
2. Add under appropriate section (Graduate Students, Undergrad, etc.):
   ```markdown
   ::: {.member-card}
   
   ![Name Photo](assets/images/team/firstname-lastname.jpg){.member-photo}
   
   ### FirstName LastName
   
   **Ph.D. Student** | Expected 2028
   
   **Research:** Brief description of research focus
   
   Bio paragraph here...
   
   :::
   ```
3. Add photo to `assets/images/team/` (square, 300x300px minimum)
4. Commit: `git commit -m "Add new PhD student: Name"`

### Moving a Student to Alumni

1. Cut their entry from the current students section
2. Paste into the Alumni section with updated format:
   ```markdown
   ::: {.alumni-card}
   
   **Dr. Name** (Ph.D. 2025)  
   *Thesis: Thesis title here*  
   **Now:** Current position
   
   :::
   ```

### Updating News on Homepage

1. Open `index.qmd`
2. Find the "Recent News" section
3. Add new item at top, remove oldest item:
   ```markdown
   - **Jan 2025** - Dr. Zhang appointed NE-2442 Senior Executive
   ```

### Changing Site Colors

Edit `styles/custom.scss`:
```scss
// MSU Maroon (current)
$primary: #5D1725;

// To change to different institution colors:
// Auburn Orange: $primary: #DD550C;
// UGA Red: $primary: #BA0C2F;
```

---

## 📤 Deployment

### Automatic (Recommended)

GitHub Actions automatically deploys when you push to `main`:

1. Push changes: `git push origin main`
2. Check progress: Repository → Actions tab
3. Site updates in ~2 minutes at https://lz245.github.io

### Manual (Backup Method)

```bash
# Render locally
quarto render

# Commit the docs folder
git add docs
git commit -m "Manual render"
git push
```

Then in GitHub Settings → Pages → Source: "Deploy from branch" → `main` → `/docs`

---

## 🏷️ Versioning & Releases

### Version Numbering

We use [Semantic Versioning](https://semver.org/):

```
v[MAJOR].[MINOR].[PATCH]

MAJOR: Complete redesign or breaking changes
MINOR: New sections, significant content additions
PATCH: Bug fixes, typos, small updates
```

### Current Version

**v1.0.0** (January 2025) - Initial release with complete lab information

### Creating a Release

When making major updates:

```bash
# 1. Update version in this README (Current Version section above)

# 2. Commit all changes
git add .
git commit -m "Prepare release v1.1.0"

# 3. Create annotated tag
git tag -a v1.1.0 -m "Release v1.1.0: Added 2025 publications and new team members"

# 4. Push with tags
git push origin main --tags
```

### Creating a GitHub Release

1. Go to repository → Releases → "Create a new release"
2. Choose existing tag (e.g., `v1.1.0`)
3. Title: `v1.1.0 - January 2025 Update`
4. Description: List major changes
5. Click "Publish release"

### Changelog

| Version | Date | Changes |
|---------|------|---------|
| v1.0.0 | Jan 2025 | Initial release: Complete site with team, publications, research, teaching |
| | | Added all current graduate students and alumni |
| | | 67+ publications |
| | | 6 research program areas |

### When to Tag a Release

- ✅ **Do tag:** New academic year updates, major content overhaul, site redesign
- ✅ **Do tag:** After adding 5+ publications, major updates
- ❌ **Don't tag:** Single typo fix, minor text edit, adding one news item

---

## 🔧 Troubleshooting

### Site not updating after push

1. Check GitHub Actions: Repository → Actions
2. Look for failed workflows (red X)
3. Common fixes:
   - YAML syntax error → Check indentation (use spaces, not tabs)
   - Missing file → Verify file paths are correct

### Images not displaying

1. Check file path matches exactly (case-sensitive)
2. Use lowercase extensions: `.jpg` not `.JPG`
3. Verify file exists in `assets/images/`

### Local preview looks different from live site

```bash
# Clear all caches
rm -rf docs _freeze .quarto

# Fresh render
quarto render
```

### "Quarto not found" error

Install Quarto: https://quarto.org/docs/get-started/

### Merge conflicts

```bash
# If you edited on GitHub and locally
git pull --rebase origin main
# Resolve conflicts in editor, then:
git add .
git rebase --continue
git push
```

---

## 📚 Resources

### Quarto Documentation
- [Quarto Websites](https://quarto.org/docs/websites/)
- [Quarto Markdown Basics](https://quarto.org/docs/authoring/markdown-basics.html)
- [Quarto Publishing](https://quarto.org/docs/publishing/github-pages.html)

### GitHub
- [GitHub Pages](https://docs.github.com/en/pages)
- [GitHub Actions](https://docs.github.com/en/actions)

### Icons
- [Bootstrap Icons](https://icons.getbootstrap.com/)
- [Emoji Cheat Sheet](https://www.webfx.com/tools/emoji-cheat-sheet/)

---

## 🙏 Acknowledgments

- Built with [Quarto](https://quarto.org) by Posit
- Hosted on [GitHub Pages](https://pages.github.com)
- Inspired by academic website best practices

---

## 📞 Contact

**Li Zhang, Ph.D.**  
Assistant Professor  
Department of Poultry Science  
Mississippi State University  

📧 l.zhang@msstate.edu  
🌐 https://lz245.github.io
