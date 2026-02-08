# Personal Academic Website — Setup & Customisation Guide

This repository contains a ready-to-use **Quarto website** template designed for
academic personal pages. It builds in **RStudio**, renders to static HTML, and is
hosted for free on **GitHub Pages**.

---

## Table of Contents

1. [Prerequisites](#1-prerequisites)
2. [Initial Setup (One-Time)](#2-initial-setup-one-time)
3. [Project Structure Explained](#3-project-structure-explained)
4. [Filling in Your Content](#4-filling-in-your-content)
5. [Building the Site Locally](#5-building-the-site-locally)
6. [Publishing to GitHub Pages](#6-publishing-to-github-pages)
7. [Day-to-Day Workflow](#7-day-to-day-workflow)
8. [Customisation Options](#8-customisation-options)
9. [Troubleshooting](#9-troubleshooting)

---

## 1. Prerequisites

Install the following before you begin:

| Software | What it does | Install link |
|----------|-------------|-------------|
| **R** (≥ 4.1) | Runtime for `.qmd` files | <https://cran.r-project.org> |
| **RStudio** (≥ 2022.07) | IDE with built-in Quarto support | <https://posit.co/download/rstudio-desktop/> |
| **Quarto** (≥ 1.3) | The document/website engine | <https://quarto.org/docs/get-started/> |
| **Git** | Version control | <https://git-scm.com/downloads> |
| **GitHub account** | Hosting | <https://github.com> |

> **Tip:** Recent versions of RStudio ship with Quarto bundled. Check by running
> `quarto --version` in the RStudio Terminal pane. If it prints a version ≥ 1.3
> you are good to go.

---

## 2. Initial Setup (One-Time)

### 2a. Clone the repository

If you haven't already cloned this repo to your machine:

```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
cd YOUR_REPO_NAME
```

### 2b. Open in RStudio

1. In RStudio: **File → Open Project…**
2. Navigate to the cloned folder and select `website.Rproj`.
3. RStudio now recognises this as a Quarto website project. You will see a
   **Build** pane (usually top-right) with a "Render Website" button.

### 2c. Add your files

- **Profile photo:** Save a square image (≥ 400 × 400 px) as `img/profile.jpg`
  (or `.png` — just update the path in `index.qmd`).
- **CV PDF:** Save your CV as `cv/your-cv.pdf` (update the filename in
  `cv.qmd` if you use a different name).
- **Working paper PDFs** (optional): Place them in `papers/`.
- **Syllabi** (optional): Place them in `teaching/`.

---

## 3. Project Structure Explained

```
website/
├── _quarto.yml          # Main configuration (site title, navbar, theme)
├── website.Rproj        # RStudio project file
├── styles.css           # All custom styling (colours, layout, cards)
├── index.qmd            # Landing / home page
├── research.qmd         # Research page (publications, working papers, etc.)
├── cv.qmd               # CV page (embedded PDF + download link)
├── teaching.qmd         # Teaching page (courses by role)
├── img/                 # Your profile photo goes here
│   └── profile.jpg
├── cv/                  # Your CV PDF goes here
│   └── your-cv.pdf
├── papers/              # Working paper PDFs (optional)
├── teaching/            # Syllabi PDFs (optional)
├── docs/                # ← Quarto output (auto-generated, served by GitHub Pages)
│   └── .nojekyll        #   Tells GitHub not to process with Jekyll
└── .gitignore
```

### Key files in detail

| File | Purpose |
|------|---------|
| `_quarto.yml` | Central config. Controls site title (shown in navbar), page order, theme, and format options. |
| `index.qmd` | Landing page. Uses a Quarto **grid layout** (`:::: {.grid}`) to place your photo on the left and bio on the right. On mobile the columns stack vertically. |
| `research.qmd` | Four sections — Publications, Working Papers, Ongoing Work, Outreach — each using styled `.publication-entry` divs. Includes collapsible abstracts and small inline buttons for links. |
| `cv.qmd` | Embeds your CV PDF in an `<iframe>` with a download button above. |
| `teaching.qmd` | Courses grouped by role (Instructor / TA). Uses `.course-entry` styled divs. |
| `styles.css` | All visual customisation. CSS variables at the top control the accent colour palette. Detailed comments explain each section. |

---

## 4. Filling in Your Content

Every `.qmd` file is heavily commented with `<!-- ... -->` HTML comments that
explain what to change. Here is a summary:

### `_quarto.yml`

- Change `title:` under `website:` to your name (this appears in the navbar).
- Optionally change the theme (see [Section 8](#8-customisation-options)).

### `index.qmd` (Landing page)

1. Replace `img/profile.jpg` with the path to your actual photo.
2. Replace "Your Name", affiliation, and department links.
3. Update the four social/academic links (Google Scholar, ORCID, Bluesky,
   University Profile) with your actual URLs. Delete or add links as needed.
4. Write your bio in the right-hand column.

### `research.qmd`

- Copy/paste the `::: {.publication-entry} ... :::` blocks for each item.
- Fill in titles, coauthors, journal names, and links.
- For working papers, write the abstract inside the `<details>` block.
- Delete any sections you don't need.

### `cv.qmd`

- Place your CV at `cv/your-cv.pdf` (or change the path in the file).
- If you prefer an HTML CV instead of an embedded PDF, follow the commented
  alternative at the bottom of the file.

### `teaching.qmd`

- Fill in course names, codes, semesters, and your role.
- Uncomment the syllabus/evaluation buttons if you want to link PDFs.
- Delete sections (e.g., Guest Lectures) you don't need.

---

## 5. Building the Site Locally

### Option A: RStudio GUI

1. Open the project in RStudio.
2. Go to the **Build** pane → click **Render Website** (or press
   `Ctrl+Shift+B` / `Cmd+Shift+B`).
3. The site renders into the `docs/` folder and opens in the Viewer pane.

### Option B: Terminal / Console

From the RStudio Terminal pane (or any terminal in the project root):

```bash
quarto render
```

### Option C: Live preview (recommended while editing)

```bash
quarto preview
```

This starts a local server (usually `http://localhost:4567`) and
**auto-refreshes** whenever you save a `.qmd` or `.css` file. Very useful for
iterating on content and design.

---

## 6. Publishing to GitHub Pages

### 6a. Configure GitHub Pages (one-time)

1. Push your repo to GitHub (if you haven't already):
   ```bash
   git add -A
   git commit -m "Initial website template"
   git push -u origin main
   ```
2. On GitHub, go to your repository → **Settings** → **Pages**.
3. Under **Source**, select:
   - **Branch:** `main`
   - **Folder:** `/docs`
4. Click **Save**.
5. GitHub will show you the URL (typically `https://YOUR_USERNAME.github.io/YOUR_REPO_NAME/`).

> **Note on custom domains:** If you want a custom domain like
> `www.yourname.com`, see GitHub's guide:
> <https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site>

### 6b. The `docs/` output folder

The `_quarto.yml` sets `output-dir: docs` so that Quarto writes all generated
HTML/CSS/JS into `docs/`. GitHub Pages serves files from this folder. The
`.nojekyll` file inside `docs/` tells GitHub to skip Jekyll processing (which
would break Quarto's output).

### 6c. Alternative: GitHub Actions (automated builds)

Instead of committing the `docs/` folder, you can have GitHub build the site
automatically on every push. This is more advanced but keeps your repo cleaner:

1. Remove `docs/` from the repo and add it to `.gitignore`.
2. In `_quarto.yml`, change `output-dir: docs` to `output-dir: _site`.
3. Create `.github/workflows/publish.yml`:

```yaml
name: Build and deploy Quarto site
on:
  push:
    branches: [main]

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: quarto-dev/quarto-actions/setup@v2
      - run: quarto render
      - uses: actions/upload-pages-artifact@v3
        with:
          path: _site
      - uses: actions/deploy-pages@v4
```

4. In GitHub repo settings → Pages → Source, select **GitHub Actions**.

The default setup in this template uses the simpler `docs/` approach (no Actions
needed).

---

## 7. Day-to-Day Workflow

Once everything is set up, your typical workflow is:

```
1. Open website.Rproj in RStudio
2. Edit .qmd files (add a paper, update teaching, etc.)
3. Preview:      quarto preview
4. Render:       quarto render        (or Build → Render Website)
5. Commit & push:
     git add -A
     git commit -m "Add new publication"
     git push
6. Wait ~1 minute for GitHub Pages to update
```

---

## 8. Customisation Options

### Theme

The site uses the **cosmo** Bootswatch theme. Quarto supports 25 built-in
themes. To switch, change the `theme:` value in `_quarto.yml`:

| Theme | Style |
|-------|-------|
| `cosmo` | Clean, modern (default) |
| `flatly` | Flat design, slightly softer |
| `litera` | Serif-influenced, scholarly feel |
| `lux` | High contrast, elegant |
| `minty` | Green accents, friendly |
| `journal` | Traditional academic look |
| `simplex` | Minimal, red accents |
| `united` | Ubuntu-inspired, warm |

Full list: <https://quarto.org/docs/output-formats/html-themes.html>

### Dark mode

Uncomment the `dark: darkly` line in `_quarto.yml` to add a light/dark toggle
to the navbar.

### Accent colour

Edit the CSS variables at the top of `styles.css`:

```css
:root {
  --accent:        #2c3e6b;   /* Change to your university colour */
  --accent-hover:  #1a2a4a;
  --accent-light:  #eef1f7;
}
```

### Profile photo shape

In `styles.css`, find `.profile-photo` and change `border-radius`:

- `50%` — circle (default)
- `8px` — rounded square
- `0` — sharp square

### Entry card style

The `.publication-entry` / `.course-entry` classes create left-bordered cards.
Alternatives:

- **Full border:** replace `border-left: 3px solid var(--accent)` with
  `border: 1px solid var(--border-color)`
- **No background:** set `background-color: transparent`
- **No cards:** remove the entire `.publication-entry` CSS rule

### Fonts

Uncomment `mainfont:` in `_quarto.yml` and add a Google Fonts `@import` at the
top of `styles.css`. Example for the Lato font:

```css
@import url('https://fonts.googleapis.com/css2?family=Lato:wght@400;700&display=swap');
```

```yaml
# in _quarto.yml
mainfont: "Lato"
```

### Adding new pages

1. Create a new `.qmd` file (e.g., `software.qmd`).
2. Add it to the navbar in `_quarto.yml`:
   ```yaml
   right:
     - text: "Research"
       href: research.qmd
     - text: "Software"        # ← new
       href: software.qmd      # ← new
     - text: "CV"
       href: cv.qmd
     - text: "Teaching"
       href: teaching.qmd
   ```
3. Render and commit.

### Adding new social links

In `index.qmd`, copy an existing `<a>` link block and change the icon class and
URL. Icons come from two CDN-loaded libraries:

- **Font Awesome 6** (brand & solid icons): <https://fontawesome.com/search>
- **Academicons** (academic service icons): <https://jpswalsh.github.io/academicons/>

Examples:

```html
<a href="https://github.com/yourname" class="social-link" target="_blank">
  <i class="fa-brands fa-github"></i> GitHub
</a>
<a href="https://x.com/yourhandle" class="social-link" target="_blank">
  <i class="fa-brands fa-x-twitter"></i> X / Twitter
</a>
<a href="https://linkedin.com/in/yourname" class="social-link" target="_blank">
  <i class="fa-brands fa-linkedin"></i> LinkedIn
</a>
<a href="mailto:you@university.edu" class="social-link" target="_blank">
  <i class="fa-solid fa-envelope"></i> Email
</a>
```

---

## 9. Troubleshooting

| Problem | Solution |
|---------|----------|
| `quarto: command not found` | Install Quarto from <https://quarto.org/docs/get-started/> or update RStudio. |
| Icons don't render | Icons are loaded from CDNs (Font Awesome + Academicons). Check your internet connection, or verify the `<link>` tags in `_quarto.yml` under `include-in-header`. |
| Site shows 404 on GitHub | Check Settings → Pages → Source is set to `main` branch, `/docs` folder. Make sure `docs/` is committed. |
| Changes don't appear on GitHub Pages | Run `quarto render`, commit `docs/`, push, and wait ~1 min. |
| PDF doesn't embed in CV page | Check the file path matches exactly (case-sensitive). Some mobile browsers don't support iframe PDFs — the download button is the fallback. |
| Profile photo looks stretched | Use a square image (same width and height). |
| Layout breaks on mobile | The grid is responsive by default. If you edited the grid classes, ensure you kept both `.g-col-12` (mobile) and `.g-col-md-4` / `.g-col-md-8` (desktop). |
| Navbar title is wrong | Change `title:` under `website:` in `_quarto.yml`. |

---

## Quick Reference: Files to Edit

| What you want to change | File to edit |
|--------------------------|-------------|
| Your name in the navbar | `_quarto.yml` → `website: title:` |
| Profile photo, bio, links | `index.qmd` |
| Publications & papers | `research.qmd` |
| CV | `cv.qmd` + replace `cv/your-cv.pdf` |
| Teaching history | `teaching.qmd` |
| Colours, fonts, layout | `styles.css` |
| Theme, dark mode, site structure | `_quarto.yml` |
