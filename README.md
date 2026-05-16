# Traders Hub — landing page

Marketing site for Traders Hub — a local-first dashboard for systematic futures traders.

Built as a single static `index.html` with Tailwind via CDN. Form capture via [Tally](https://tally.so). Hosted on GitHub Pages.

## Deploy

1. **Create a Tally form** at https://tally.so with one Email field.
2. **Edit `index.html`** — find the `<script>` block near the bottom, replace `TALLY_FORM_ID` with your Tally form ID (the part after `tally.so/r/` in the form URL), and confirm `EMAIL_FIELD_LABEL` matches your Tally form's field label exactly.
3. **Push to GitHub Pages** — see "GitHub setup" below.

## GitHub setup

```bash
cd ~/tradershub-landing
git init -b main
git add .
git commit -m "Initial landing page"

# Create the public repo (requires gh CLI)
gh repo create tradershub-landing --public --source=. --push \
  --description="Landing page for Traders Hub"

# Enable Pages via the GitHub web UI:
#   Settings → Pages → Source: Deploy from a branch → main → / (root) → Save
# After 1-2 minutes the site is live at:
#   https://<your-username>.github.io/tradershub-landing/
```

## Custom domain (optional)

1. Buy `tradershub.app` from any registrar (~$15/year on Cloudflare Registrar)
2. Add a `CNAME` file to this repo with one line: `tradershub.app`
3. In your DNS provider, point `tradershub.app` to GitHub Pages' IPs:
   - 185.199.108.153
   - 185.199.109.153
   - 185.199.110.153
   - 185.199.111.153
4. In GitHub repo → Settings → Pages → Custom domain → enter `tradershub.app`, save
5. Wait 5-10 minutes, then check "Enforce HTTPS"

## Local preview

```bash
python3 -m http.server 8080
# open http://localhost:8080
```

## Updating

Edit `index.html`, then:

```bash
git add . && git commit -m "Tweak copy" && git push
```

GitHub Pages rebuilds in 30-60 seconds.

## Live deployment state (as of 2026-05-16)

This is the live-config snapshot — keep it current as things change.

| What | Value |
|---|---|
| Live URL | https://traders-hub.io |
| GitHub repo | https://github.com/dbraxton2621/tradershub-landing |
| Hosting | GitHub Pages, `main` branch, `/` (root) |
| Custom domain | `traders-hub.io` (apex), set in repo Settings → Pages |
| HTTPS enforced | yes |
| DNS registrar | Squarespace Domains |
| Form provider | [Tally](https://tally.so) |
| Tally form ID | `EkZXvl` (see `index.html` line ~394, constant `TALLY_FORM_ID`) |
| Tally field label | `Email` (constant `EMAIL_FIELD_LABEL`) |
| Pre-fill mechanism | Form on the landing page captures email, then opens `https://tally.so/r/EkZXvl?Email=<encoded>` in a new tab so Tally records the submission |

### DNS records (at Squarespace)

Apex `traders-hub.io` → four A records pointing at GitHub Pages:

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

`www.traders-hub.io` — optional CNAME to `dbraxton2621.github.io`. Not currently configured; the apex is the canonical URL.

### Asset map

| File | Purpose |
|---|---|
| `index.html` | The entire site — single file, Tailwind via CDN |
| `CNAME` | Tells GitHub Pages the custom domain (contents: `traders-hub.io`) |
| `full-logo.png` | Original 2064×512 source logo (TH crystal + wordmark). Don't delete — used to regenerate the favicon set. |
| `logo-mark.png` | 1024×1024 cropped TH symbol, transparent background. Master for the favicon set. |
| `favicon.ico` | Multi-res 16/32/48 |
| `favicon-{16,32,180,192,512}.png` | Sized variants linked in `<head>` |
| `apple-touch-icon.png` | 180×180 for iOS home screens |

### Regenerating favicons after a new logo

If you replace `full-logo.png`, regenerate everything else with the Python crop pattern documented in `~/tradingview-mcp/SESSION_NOTES.md` (the "Logo / favicon regeneration" section). The TL;DR is: detect the natural vertical gap between TH symbol and wordmark, crop to the left of the gap, make the black background transparent, then resize down to all favicon sizes.

### Common operations

- **Push from sandbox/Linux without creds**: not possible. Push from the Mac (`git push` uses macOS keychain) or use a fine-scoped GitHub PAT.
- **DNS shows old values after a change**: TTL is typically 4 hours at Squarespace. Browser/OS/cellular caches add more. Wait, or use a different network to verify.
- **Tally submission missing**: check the field label in Tally exactly matches `EMAIL_FIELD_LABEL` in the script. Tally is case-sensitive on labels.
