# TDS / wt% Converter — PWA

A Progressive Web App for converting between TDS (mg/L) and weight percent for NaCl, MgSO₄, custom ion compositions, and fixed-density solutions, with full temperature correction.

## Features

- **NaCl** — Rogers & Pitzer (1982) density model, 0–100 °C, 0–26.4 wt%
- **MgSO₄** — Connaughton et al. (1986) density model, 0–80 °C, 0–21.4 wt%
- **Custom ions** — 12 cations (Na⁺, Ca²⁺, Mg²⁺, K⁺, Li⁺, Fe²⁺, Fe³⁺, Mn²⁺, Al³⁺, Sr²⁺, Ba²⁺, NH₄⁺) + 10 anions (Cl⁻, SO₄²⁻, HCO₃⁻, CO₃²⁻, NO₃⁻, PO₄³⁻, F⁻, Br⁻, SiO₂, B), TDS by direct sum, wt% via supplied density
- **Fixed ρ** — arbitrary solution with user-supplied constant density
- Bidirectional conversion (TDS ↔ wt%)
- °C / °F temperature toggle
- Reference table updates live with temperature
- Fully offline after first load (service worker cache)
- Installable on Windows PC, Android, and iOS

---

## File structure

All 5 files sit in the root — no subfolders required:

```
index.html       ← entire app (HTML + CSS + JS)
manifest.json    ← PWA metadata (name, icons, colors)
sw.js            ← service worker (offline caching)
icon-192.png     ← home screen icon (Android / general)
icon-512.png     ← high-res icon (splash screens)
```

---

## Deploying to GitHub Pages

### What you need
- A free GitHub account at https://github.com
- Git installed on your PC — download from https://git-scm.com if needed (optional; web upload works fine)

---

### Step 1 — Create a new repository

1. Go to https://github.com and sign in
2. Click the **+** icon (top right) → **New repository**
3. Name it: `tds-converter`
4. Set visibility to **Public** (required for free GitHub Pages)
5. Leave all other options at their defaults — do not add a README or .gitignore
6. Click **Create repository**

---

### Step 2 — Upload the files

**Option A — GitHub web interface (no Git required)**

1. On your new empty repository page, click **Add file → Upload files**
2. Unzip the downloaded package and drag all 5 files directly onto the upload area:
   - `index.html`
   - `manifest.json`
   - `sw.js`
   - `icon-192.png`
   - `icon-512.png`
   - `README.md` (this file — optional but recommended)
3. Add a commit message such as `Initial upload`
4. Click **Commit changes**

**Option B — Git command line**

Open a terminal or Git Bash in the folder containing the 5 files, then run:

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/tds-converter.git
git push -u origin main
```

Replace `YOUR_USERNAME` with your actual GitHub username.

---

### Step 3 — Enable GitHub Pages

1. In your repository, click **Settings** (top navigation bar)
2. Click **Pages** in the left sidebar
3. Under **Source**, select **Deploy from a branch**
4. Set Branch to **main** and folder to **/ (root)**
5. Click **Save**
6. Wait 1–2 minutes — your app will be live at:

```
https://YOUR_USERNAME.github.io/tds-converter/
```

GitHub shows the live URL at the top of the Pages settings once deployment is complete.

---

## Installing on each device

### Windows PC (Chrome or Edge)
1. Open the URL in Chrome or Edge
2. Click the install icon (⊕) in the address bar, or open the three-dot menu → **Install TDS Converter**
3. Click **Install** — the app opens as a standalone window and appears in your Start menu

### Android (Chrome)
1. Open the URL in Chrome
2. Tap the three-dot menu → **Add to Home screen**
3. Tap **Add** — the icon appears on your home screen and the app opens full-screen

### iPhone / iPad (must use Safari — not Chrome)
1. Open the URL in **Safari**
2. Tap the **Share** button (box with arrow pointing up, bottom of screen)
3. Scroll down and tap **Add to Home Screen**
4. Tap **Add** — the icon appears on your home screen

> **Note:** On iOS, PWA installation only works from Safari. Chrome and other browsers on iPhone do not support the Add to Home Screen flow for PWAs.

---

## Offline use

After the first load on any device, the app is fully cached by the service worker and works without an internet connection. No data is sent anywhere — all calculations run locally in the browser.

---

## Updating the app

When you make changes to any file:

1. Open `sw.js` and increment the cache version — change `tds-converter-v1` to `tds-converter-v2` (increment each time you update)
2. Upload the changed files to GitHub (drag-and-drop upload or `git push`)
3. GitHub Pages redeploys within 1–2 minutes
4. On next open, devices automatically receive the updated version
