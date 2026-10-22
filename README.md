# Everyday Calculator

A basic calculator built as an installable Progressive Web App (PWA). It's a static site with no build step and no dependencies. People can install it on their phone's home screen, and it works offline.

- Add, subtract, multiply, divide, decimals, percent, sign toggle, backspace and all-clear
- Keyboard support: digits, `+ - * /`, `Enter` for equals, `Backspace` to delete, `Esc` to clear
- History tape of finished calculations (saved on the device); tap an entry to reuse its result
- Installable on Android, iPhone, iPad and desktop, opens full-screen like a native app
- Works offline after the first visit
- Light and dark themes that follow the system setting

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The whole app: markup, styles, calculator logic, install prompt |
| `manifest.webmanifest` | App name, colours and icons used when installing |
| `sw.js` | Service worker that caches the app for offline use |
| `icons/` | Home-screen icons (standard, maskable for Android, Apple touch icon, SVG) |
| `_headers` | Cloudflare Pages headers: security, and no caching on `sw.js` so updates arrive |
| `.gitignore` | Keeps local and tooling files out of the repo |

## Run locally

Service workers need `http://localhost` or HTTPS, so serve the folder instead of opening the file directly:

```bash
python3 -m http.server 8080
```

Then visit http://localhost:8080.

## Publish to GitHub

```bash
cd everyday-calculator
git init -b main
git add .
git commit -m "Add Everyday Calculator PWA"
git remote add origin https://github.com/<your-username>/everyday-calculator.git
git push -u origin main
```

Create the empty `everyday-calculator` repository on GitHub first, without a README, so the push is clean.

## Deploy on Cloudflare Pages

1. In the Cloudflare dashboard, go to **Workers & Pages**, then **Create**, then the **Pages** tab, then **Connect to Git**.
2. Pick the `everyday-calculator` repository.
3. Set **Framework preset** to `None`, leave **Build command** empty, and set **Build output directory** to `/` (or leave it blank).
4. Choose **Save and Deploy**. Every push to `main` redeploys the site.
5. For a custom domain, open the project, choose **Custom domains**, then **Set up a custom domain**.

Cloudflare serves every site over HTTPS, which PWAs require.

Command-line alternative:

```bash
npx wrangler pages deploy . --project-name everyday-calculator
```

## Installing on a phone

- **Android (Chrome, Edge, Samsung Internet):** the app shows an **Install** button at the top. You can also use the browser menu and choose **Install app** or **Add to Home screen**.
- **iPhone and iPad (Safari):** the app shows a short hint. Tap **Share**, then **Add to Home Screen**.
- **Desktop (Chrome, Edge):** use the **Install** button, or the install icon in the address bar.

Visitors can dismiss the install card with ×, and it stays hidden on that device. It never appears once the app is installed.

## Releasing an update

1. Change the files.
2. In `sw.js`, bump `VERSION` (for example `v1.0.0` to `v1.0.1`).
3. Commit and push. Installed copies pick up the new version the next time they're opened online.

## Customising

All colours are CSS variables at the top of the `<style>` block in `index.html`. There's a light set, and a dark set that applies automatically when the visitor's system uses dark mode. If you change the background colour, update `background_color` and `theme_color` in `manifest.webmanifest`, and the two `theme-color` meta tags in `index.html`. The calculation logic sits between the `// <core>` and `// </core>` comments in the script.
