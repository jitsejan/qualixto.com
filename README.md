# qualixto.co.uk

Marketing site for Qualixto Ltd: a single static `index.html`, no build step.

Canonical domain is **qualixto.com**; **qualixto.co.uk** redirects to it.

## Deploy

Pushes to `main`/`master` deploy automatically to GitHub Pages via
`.github/workflows/deploy.yml`. The `CNAME` file points GitHub Pages at
`qualixto.com`; GitHub reads it automatically on deploy.

One-time setup:

1. In the GitHub repo, go to **Settings → Pages** and set the source to
   **GitHub Actions**. (Already done for this repo.)
2. In **Cloudflare DNS** for `qualixto.com` (the primary domain), add:
   - `CNAME` record `@` → `<username>.github.io`, proxied.
   - `CNAME` record `www` → `<username>.github.io`, proxied.
   - Or follow [GitHub's custom domain docs](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site)
     for the apex-domain A/AAAA record variant if `@` CNAME flattening isn't
     supported on your plan (Cloudflare supports CNAME flattening, so `@` → GitHub
     Pages works directly).
   - In GitHub repo **Settings → Pages**, set the custom domain to
     `qualixto.com` and enable **Enforce HTTPS** once DNS has propagated.
3. In **Cloudflare** for `qualixto.co.uk` (the redirecting domain), do **not**
   point it at GitHub Pages: GitHub Pages only serves the one domain named in
   `CNAME`. Instead, use a Cloudflare **Bulk Redirect** (or a Page Rule) on
   `qualixto.co.uk/*` → `https://qualixto.com/$1` (301, preserve path/query).
   Keep DNS for `qualixto.co.uk` proxied (orange cloud) so the redirect rule
   can intercept the request.

## Before going live

- [x] Booking link in `index.html` (`#book` section) points to the real
      Google Calendar booking page.
- [ ] Confirm `contact@qualixto.com` is set up in Google Workspace and receiving mail.
- [x] Verify DNS + HTTPS on qualixto.com (GitHub Pages auto-provisions a cert
      once DNS resolves).
- [x] Verify qualixto.co.uk redirects (301) to the equivalent qualixto.com page.

## qualixto.co.uk email

Not set up, and intentionally out of scope. `qualixto.co.uk` is kept registered
and redirecting purely for brand protection (so it can't be squatted), but all
real email goes through `qualixto.com`. Adding it as a Google Workspace domain
alias hit a "domain already used as an alias or domain" error tied to a
pre-existing `google-site-verification` TXT record; not worth chasing further
given the domain isn't used for anything but the redirect.
