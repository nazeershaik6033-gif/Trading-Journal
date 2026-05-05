# Nazeer Trades — Trading Journal PWA

A refined, mobile-first trading journal Progressive Web App. Works offline once installed. All data lives in your browser's local storage — nothing leaves your device.

## What's in this folder

```
pwa/
├── index.html          ← Main app (React + JSX, all logic embedded)
├── manifest.json       ← PWA manifest (name, icons, theme)
├── sw.js               ← Service worker (offline support + caching)
├── icon-192.png        ← App icon (192×192)
├── icon-512.png        ← App icon (512×512)
├── icon-maskable.png   ← Maskable icon for Android adaptive icons
├── apple-touch-icon.png ← iOS home-screen icon (180×180)
└── favicon.png         ← Browser tab icon
```

## How to publish (pick one)

PWAs require **HTTPS** (except on `localhost`). Pick any of these free options.

### Option 1 — Netlify Drop (fastest, no signup)

1. Go to https://app.netlify.com/drop
2. Drag this whole `pwa` folder onto the page
3. Done. You get a public HTTPS URL like `cheery-cobbler-1234.netlify.app`

### Option 2 — Vercel

1. Push the folder to a GitHub repo
2. Go to https://vercel.com/new and import the repo
3. Deploy. You get `your-project.vercel.app`

### Option 3 — GitHub Pages

1. Create a new GitHub repo, upload the contents of this folder to the root
2. Settings → Pages → Source: `main` branch, `/ (root)` → Save
3. Visit `https://YOUR_USERNAME.github.io/REPO_NAME/`

### Option 4 — Cloudflare Pages

1. Push to GitHub, connect at https://pages.cloudflare.com
2. Build settings: leave blank (it's static)

### Option 5 — Local test (without publishing)

```bash
cd pwa
python3 -m http.server 8000
# Open http://localhost:8000 on your computer
```

For testing on your phone over local Wi-Fi, use your computer's local IP
(e.g. `http://192.168.1.5:8000`). Note: service worker / install requires
HTTPS or `localhost`, so phone testing over plain HTTP won't install as PWA
but the app still runs.

## Installing on your phone

Once it's published at an HTTPS URL:

**iPhone (Safari):**
1. Open the URL in Safari
2. Tap the Share button
3. Tap "Add to Home Screen"

**Android (Chrome):**
1. Open the URL in Chrome
2. Tap the menu (⋮) → "Install app" or "Add to Home screen"

**Desktop (Chrome / Edge):**
1. Open the URL
2. Click the install icon in the address bar (looks like a monitor with a down arrow)

After install, the app runs full-screen, works offline, and lives on your home screen like any native app.

## How your data is stored

- All trades, watchlist items, strategies, and settings are saved in your browser's `localStorage` on the device where you installed the app.
- Use **More → Settings → Backup & Restore** to export your full journal as a JSON file. Save that file somewhere safe (cloud drive, email to yourself, etc.).
- To restore on a new device or after clearing browser data, install the app and import your JSON.

## Updating the app

When you change any file in the `pwa/` folder:

1. Bump the `VERSION` constant in `sw.js` (e.g. `nazeer-trades-v1.0.1` → `nazeer-trades-v1.0.2`)
2. Re-deploy
3. Users will pick up the new version on their next visit

## Customizing

- **App name / colors:** Edit `manifest.json`
- **Icons:** Replace the PNGs with your own (keep filenames + sizes)
- **App logic:** All React/JSX is inside `index.html` between the `<script type="text/babel">` tags

## Tech notes

- React 18 + Recharts + Lucide icons, all loaded via ESM CDN (esm.sh)
- Tailwind CSS via CDN
- JSX transpiled in-browser by Babel Standalone
- No build step. No npm. No bundler. Just static files.
- Service worker uses cache-first for app shell, stale-while-revalidate for CDN modules.

## Privacy

Nazeer Trades runs entirely in your browser. There is no backend, no analytics, no telemetry. Your trading data never leaves your device unless you explicitly export it.
