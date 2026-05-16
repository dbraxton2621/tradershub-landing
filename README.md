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
