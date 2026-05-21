# Gensyn Design System

Brand UI kit extracted from the Gensyn diagnostic tool: colours, Inter typography, lavender gradient background, white cards, forms, and results patterns.

**Live style guide (after you deploy):** `https://<your-org>.github.io/gensyn-design-system/`

---

## What you need to do (one-time setup)

Follow these steps to publish this as its own GitHub repo and share it with your team.

### Step 1 — Create a new GitHub repository

1. On GitHub: **New repository** → name it `gensyn-design-system` (or your preferred name).
2. Set it **Public** (required for free GitHub Pages) or Private with GitHub Enterprise Pages.
3. Do **not** add a README, .gitignore, or license (this folder already has them).

### Step 2 — Push this folder to that repo

From your machine (PowerShell), in the **FitFinderC** repo root:

```powershell
cd C:\Developer\FitFinderC\design-system

git init
git add .
git commit -m "Initial Gensyn design system — tokens, CSS, style guide"
git branch -M main
git remote add origin https://github.com/YOUR_ORG/gensyn-design-system.git
git push -u origin main
```

Replace `YOUR_ORG` with your GitHub username or organisation.

> **Note:** This folder is intentionally separate from `gensyn-diagnostic`. You can keep a copy here for reference and treat the new repo as the canonical source.

### Step 3 — Enable GitHub Pages

1. Repo → **Actions** → confirm **“Deploy style guide to GitHub Pages”** ran green on `main` (re-run if needed: **Run workflow**).
2. Repo → **Settings** → **Pages**
3. **Build and deployment** → Source: **Deploy from a branch**
4. Branch: **`gh-pages`** · Folder: **`/ (root)`** → **Save**
5. Wait 1–2 minutes, then open: **https://samgs2.github.io/gensyn-design-system/**

If you still see 404: Pages source must be **`gh-pages`**, not `main`. The workflow publishes the style guide to the `gh-pages` branch automatically.

### Step 4 — Share with your boss and team

- **Boss / stakeholders:** send the Pages URL only — it shows colours, type, and components.
- **Developers:** clone the repo or add as submodule.
- **Claude Code / Cursor:** copy `CLAUDE.md.template` → `CLAUDE.md` in each new project (see below).

### Step 5 — Optional: tag a release

```powershell
git tag v1.0.0
git push origin v1.0.0
```

Other repos can pin to `v1.0.0` when using a submodule.

---

## Repo contents

```
design-system/
├── tokens/           # JSON — colours, type, spacing (for tooling / AI)
├── css/
│   ├── gensyn-tokens.css      # Variables + .gensyn-page shell
│   └── gensyn-components.css  # .gensyn-card, buttons, forms, etc.
├── assets/
│   └── gensyn-logo.svg
├── docs/             # GitHub Pages site (static style guide)
├── examples/react/   # Copy-paste Vite notes
├── CLAUDE.md.template
└── README.md
```

---

## Adopting in a new project

### Quick (copy files)

1. Copy `css/`, `assets/`, and optionally `tokens/` into your app.
2. Import in your main CSS:

```css
@import './styles/gensyn-tokens.css';
@import './styles/gensyn-components.css';
```

3. Use on the root element:

```html
<body class="gensyn-page">
```

4. Build UI with classes from the style guide (`.gensyn-card`, `.gensyn-btn-primary`, …).

### Git submodule (teams)

```bash
git submodule add https://github.com/YOUR_ORG/gensyn-design-system.git packages/gensyn-design-system
```

```css
@import '../packages/gensyn-design-system/css/gensyn-tokens.css';
@import '../packages/gensyn-design-system/css/gensyn-components.css';
```

### Preview locally (before Pages deploy)

```powershell
cd C:\Developer\FitFinderC\design-system
Copy-Item -Recurse -Force css docs\css
Copy-Item -Recurse -Force assets docs\assets
cd docs
python -m http.server 8080
# Visit http://localhost:8080
```

(GitHub Actions copies `css/` and `assets/` into `docs/` on each deploy — same layout.)

---

## Using with Claude Code / Cursor

**Do not** paste the whole FitFinder frontend into the prompt.

**Do:**

1. Put this design system **inside the project** (copy or submodule).
2. Copy `CLAUDE.md.template` → `CLAUDE.md` in the project root.
3. Edit the style guide URL and paths in `CLAUDE.md`.
4. Prompt example:

```text
Read CLAUDE.md and packages/gensyn-design-system/README.md.
Build a settings page using Gensyn classes only — gensyn-card, gensyn-btn-primary, Inter, navy headings.
Match the published style guide. No new hex colours.
```

Claude reads files from the repo each session — consistent output across projects.

---

## CSS class reference (prefix `gensyn-`)

| Class | Use |
|-------|-----|
| `.gensyn-page` | Page shell (gradient bg, Inter, min-height) |
| `.gensyn-app` | Centered flex layout (matches diagnostic `.app`) |
| `.gensyn-bg-animated` | Optional fixed Colorflow iframe layer (intake) |
| `.gensyn-container` | Max-width 1120px wrapper |
| `.gensyn-card` | White content panel |
| `.gensyn-card--intake` | Smaller intake variant |
| `.gensyn-h1`, `.gensyn-h2`, `.gensyn-subtitle` | Typography |
| `.gensyn-btn-primary` | Navy full-width CTA |
| `.gensyn-input`, `.gensyn-textarea` | Form fields |
| `.gensyn-option` + `.selected` | Multiple-choice chips |
| `.gensyn-progress` / `.gensyn-progress-fill` | Top progress bar |
| `.gensyn-badge`, `.gensyn-section-label` | Results labels |
| `.gensyn-logo`, `.gensyn-logo--intake` | Logo sizing |

Variables: `--gensyn-navy`, `--gensyn-purple`, `--gensyn-bg-gradient`, etc. — see `css/gensyn-tokens.css`.

---

## Page background

**Static gradient (default on every page)** — in `gensyn-tokens.css`:

```css
/* #edf0fb → #f5eef9 at 160deg, fixed to viewport */
var(--gensyn-bg-gradient);
```

Apply `class="gensyn-page"` on `<body>`. Gradient is set on both `html` and `body` so it fills the screen behind white `.gensyn-card` panels.

**Animated layer (intake only)** — add before your container:

```html
<div class="gensyn-bg-animated" aria-hidden="true">
  <iframe src="https://colorflow-embed.b-cdn.net/embed.html#e=wvk6jmkA"
    width="1600" height="1200" title="" style="border:0"></iframe>
</div>
```

See the **Background** section on the [style guide](https://samgs2.github.io/gensyn-design-system/#background) for a live preview.

---

## Updating the system

1. Change tokens in `tokens/*.json` and mirror in `css/gensyn-tokens.css`.
2. Adjust components in `css/gensyn-components.css`.
3. Refresh `docs/index.html` if you add new swatches.
4. Commit, push, tag `v1.x.x`.
5. Pull submodule / re-copy in downstream apps.

---

## Source

Extracted from [gensyn-diagnostic](https://github.com/SamGS2/gensyn-diagnostic) (`frontend/src/App.css`, `ResultsPage.jsx` tokens).
