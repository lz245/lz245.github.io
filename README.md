# Zhang Lab Website

Professional academic research lab website built with [Quarto](https://quarto.org) and hosted on GitHub Pages.

## 📁 Project Structure

```
lab-website/
├── _quarto.yml              # Main site configuration
├── index.qmd                # Homepage
├── research.qmd             # Research programs
├── publications.qmd         # Auto-generated publication list
├── team.qmd                 # Lab members (reads from YAML)
├── teaching.qmd             # Courses and mentoring
├── join.qmd                 # Prospective students page
├── cv.qmd                   # CV page
├── publications.bib         # BibTeX file for publications
│
├── _data/
│   └── team.yml             # Structured team member data
│
├── assets/
│   ├── images/
│   │   ├── team/            # Member photos (150x150px recommended)
│   │   └── ...              # Other images
│   └── cv/
│       ├── cv.docx          # Source CV (Word document)
│       └── cv.pdf           # Generated PDF (auto-created)
│
├── styles/
│   ├── custom.scss          # Site styling (edit colors here)
│   └── apa-cv.csl           # Citation style
│
├── .github/
│   └── workflows/
│       └── publish.yml      # GitHub Actions for auto-deploy
│
└── docs/                    # Output directory (GitHub Pages serves from here)
```

## 🚀 Quick Start

### Prerequisites

- [R](https://www.r-project.org/) (4.0+)
- [Quarto](https://quarto.org/docs/get-started/) (1.4+)
- [Git](https://git-scm.com/)
- R packages: `yaml`, `glue`, `knitr`, `bib2df`, `dplyr`

### Local Development

1. **Clone the repository**
   ```bash
   git clone https://github.com/lz245/lz245.github.io.git
   cd lz245.github.io
   ```

2. **Install R packages**
   ```r
   install.packages(c("yaml", "glue", "knitr", "bib2df", "dplyr"))
   ```

3. **Preview locally**
   ```bash
   quarto preview
   ```
   This opens a live preview at `http://localhost:4567`

4. **Render the site**
   ```bash
   quarto render
   ```
   Output goes to the `docs/` folder

### First-Time Setup

1. **Update `_quarto.yml`**
   - Change site title, description, URL
   - Add your Google Analytics ID
   - Update social links
   - Adjust institution colors in `styles/custom.scss`

2. **Update team data**
   - Edit `_data/team.yml` with your lab members
   - Add photos to `assets/images/team/`

3. **Add your CV**
   - Place your CV as `assets/cv/cv.docx`
   - GitHub Actions will auto-convert to PDF on push

4. **Update publications**
   - Replace `publications.bib` with your BibTeX file
   - Export from Zotero, Mendeley, or Google Scholar

5. **Customize content**
   - Edit each `.qmd` file with your information

---

## 📤 Deployment to GitHub Pages

### Method 1: GitHub Actions (Recommended)

The included workflow auto-deploys on every push to `main`.

1. **Enable GitHub Pages**
   - Go to repository Settings → Pages
   - Source: "GitHub Actions"

2. **Push your changes**
   ```bash
   git add .
   git commit -m "Initial site setup"
   git push origin main
   ```

3. **Wait for deployment**
   - Check Actions tab for build status
   - Site available at `https://USERNAME.github.io/REPO-NAME/`

### Method 2: Manual Deploy

1. Render locally: `quarto render`
2. Commit the `docs/` folder
3. In Settings → Pages, set source to "Deploy from branch" → `main` → `/docs`

---

## 🌐 Custom Domain Setup

### Option A: University Subdomain (Recommended)

Contact your IT department to request a CNAME record:

```
lilab.msstate.edu → YOUR-USERNAME.github.io
```

Then:

1. Create a `CNAME` file in your repo root containing:
   ```
   lilab.msstate.edu
   ```

2. Update `_quarto.yml`:
   ```yaml
   website:
     site-url: "https://lilab.msstate.edu"
   ```

3. In GitHub Settings → Pages → Custom domain, enter `lilab.msstate.edu`

4. Enable "Enforce HTTPS"

### Option B: Personal Domain

1. Purchase domain (e.g., from Namecheap, Google Domains)

2. Add DNS records:
   ```
   Type: A
   Name: @
   Value: 185.199.108.153
          185.199.109.153
          185.199.110.153
          185.199.111.153

   Type: CNAME
   Name: www
   Value: YOUR-USERNAME.github.io
   ```

3. Follow steps 1-4 from Option A with your domain

---

## 📝 Maintenance Guide

### Adding a New Team Member

1. Edit `_data/team.yml`:
   ```yaml
   graduate_students:
     - name: "New Student"
       title: "Ph.D. Candidate"
       role: "phd"
       photo: "assets/images/team/new-student.jpg"
       email: "new.student@msstate.edu"
       research_focus: "Their research topic"
       expected_graduation: "Spring 2028"
       bio: |
         Bio text here...
   ```

2. Add photo to `assets/images/team/` (square, 300x300px minimum)

3. Commit and push

### Adding Publications

1. Export BibTeX from your reference manager

2. Replace or append to `publications.bib`

3. Publications page auto-updates on rebuild

### Updating Your CV

1. Replace `assets/cv/cv.docx` with your updated Word document

2. Push to GitHub

3. GitHub Actions automatically converts to PDF

### Changing Site Colors

Edit `styles/custom.scss`:

```scss
$primary: #660000;    // Main color (headers, links)
$accent: #d4a017;     // Accent color
```

Common institutional colors:
- MSU Maroon: `#660000`
- LSU Purple: `#461d7c`
- Auburn Orange: `#DD550C`
- Georgia Red: `#BA0C2F`

---

## 🔧 Troubleshooting

### Build fails on GitHub Actions

1. Check the Actions tab for error messages
2. Common issues:
   - Missing R packages → Add to workflow file
   - BibTeX syntax errors → Validate your `.bib` file
   - YAML indentation → Use spaces, not tabs

### Publications not showing

1. Verify `publications.bib` exists and has valid entries
2. Check R console for `bib2df` errors during local render
3. Ensure BibTeX entries have required fields (author, year, title)

### Team photos not displaying

1. Verify file path matches `_data/team.yml`
2. Check file permissions
3. Use lowercase extensions (`.jpg`, not `.JPG`)

### Local preview different from deployed site

1. Clear Quarto cache: `rm -rf _freeze .quarto`
2. Re-render: `quarto render`
3. Check for absolute vs. relative paths

---

## 📊 Analytics

Google Analytics (GA4) is pre-configured. To enable:

1. Create a GA4 property at [analytics.google.com](https://analytics.google.com)
2. Get your Measurement ID (format: `G-XXXXXXXXXX`)
3. Update `_quarto.yml`:
   ```yaml
   google-analytics:
     tracking-id: "G-XXXXXXXXXX"
   ```

---

## 📚 Resources

- [Quarto Website Documentation](https://quarto.org/docs/websites/)
- [GitHub Pages Documentation](https://docs.github.com/en/pages)
- [Bootstrap Icons](https://icons.getbootstrap.com/) (for icon codes)
- [Academicons](https://jpswalsh.github.io/academicons/) (ORCID, Google Scholar icons)

---

## 📄 License

Content © 2025 [Your Name]. Website template structure available under MIT license.

---

## 🙏 Acknowledgments

Built with [Quarto](https://quarto.org) by Posit. Inspired by academic website best practices from the research community.
