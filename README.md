# Everyday Calculator

A basic calculator in a single static page. No build step, no dependencies.

- Add, subtract, multiply, divide, decimals, percent, sign toggle, backspace and all-clear
- Keyboard support: digits, `+ - * /`, `Enter` for equals, `Backspace` to delete, `Esc` to clear
- History tape of finished calculations (saved in the browser); tap an entry to reuse its result
- Responsive layout for phones, light and dark themes that follow the system setting

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The whole app: markup, styles and script |
| `_headers` | Security headers for Cloudflare Pages |
| `.gitignore` | Keeps local and tooling files out of the repo |

## Run locally

Open `index.html` in a browser, or serve the folder:

```bash
python3 -m http.server 8080
```

Then visit http://localhost:8080.

## Publish to GitHub

```bash
cd everyday-calculator
git init -b main
git add .
git commit -m "Add Everyday Calculator"
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

### Alternative: deploy from the command line

```bash
npx wrangler pages deploy . --project-name everyday-calculator
```

## Customising

All colours are CSS variables at the top of the `<style>` block in `index.html`, with a light set, and a dark set that applies automatically when the visitor's system uses dark mode. The calculation logic sits between the `// <core>` and `// </core>` comments in the script.
