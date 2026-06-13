# Begena Radio — ቤግና ሬዲዮ

24/7 Ethiopian Pentecostal gospel internet radio for the Habesha diaspora in the DMV.

## Architecture

| Layer | Domain | Host |
|-------|--------|------|
| Website (this repo) | `begenaradio.com` | Cloudflare Pages |
| Stream server | `radio.begenaradio.com` | AzuraCast on Hetzner VPS |

## Deploy to Cloudflare Pages

### First deploy

```bash
npx wrangler pages deploy . --project-name begena-radio
```

When prompted, select **Create a new project** and choose the production branch.

### Subsequent deploys

```bash
npx wrangler pages deploy . --project-name begena-radio
```

### Via GitHub (auto-deploy)

1. Push this repo to GitHub.
2. In Cloudflare Pages → Create Project → Connect to Git → select the repo.
3. Build command: *(leave empty)*  
4. Build output directory: `/` (root)
5. Every push to `main` auto-deploys.

## Local preview

```bash
npx wrangler pages dev .
```

## File structure

```
index.html          # Player (gospel-radio-player.html, AZURACAST URL changed)
manifest.webmanifest
sw.js               # Service worker — caches shell, never caches stream/API
_headers            # Cloudflare Pages cache + security headers
assets/
  begena-logo.svg
  icon-192.png
  icon-512.png
  icon-1200.png     # OG image
  favicon.ico
```

## Regenerate icons

```bash
node generate-icons.mjs
node generate-favicon.mjs
```

Requires `@resvg/resvg-js` (`npm install`).

## Phase 2 — Server setup

See `server/SETUP.md` for AzuraCast installation on Hetzner VPS.
