# qualixto.co.uk

Marketing site for Qualixto Ltd — a single static `index.html`, no build step.

## Deploy

Pushes to `main`/`master` deploy automatically to GitHub Pages via
`.github/workflows/deploy.yml`.

One-time setup:

1. In the GitHub repo, go to **Settings → Pages** and set the source to
   **GitHub Actions**.
2. In **Cloudflare DNS** for `qualixto.co.uk`, add:
   - `CNAME` record `@` (or `www`) → `<username>.github.io`, proxied.
   - Or follow [GitHub's custom domain docs](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site)
     for the apex-domain A/AAAA record variant if `@` CNAME flattening isn't
     supported on your plan (Cloudflare supports CNAME flattening, so `@` → GitHub
     Pages works directly).
3. The `CNAME` file in this repo already points to `qualixto.co.uk` — GitHub
   Pages reads it automatically on deploy.

## Before going live

- [ ] Replace the placeholder booking link in `index.html` (`#book` section)
      with a real Cal.com/Calendly URL.
- [ ] Confirm `hello@qualixto.co.uk` is a real, monitored inbox.
- [ ] Verify DNS + HTTPS (GitHub Pages auto-provisions a cert once DNS resolves).
