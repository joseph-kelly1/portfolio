# Deployment Handoff (for Stage 6, Codex)

Prepared by Claude Code on 2026-10-14 at the end of Stage 5. Nothing has been provisioned, deployed, or changed in DNS.

## Release status

Joseph authorized Railway hosting and Cloudflare DNS setup on 2026-10-14 after the UI revisions. He explicitly approved publishing both email addresses and current project updates to GitHub and the public site. Deployment is in progress.

## What to serve

- **Public directory:** `public/`. Serve it as the site root.
- **Application build step:** none. Railway Railpack detects `Staticfile`, serves only `public/` with Caddy, and reads healthcheck/restart settings from `railway.json`. No bundler, framework, or package install is needed for site content.
- **Generated assets:** only `public/assets/resume-portfolio.pdf`, which is **committed**. It is built from `resume/resume-portfolio.tex` with pdfLaTeX (command in `README.md`). Deployment must not depend on rebuilding it. Rebuild only when the résumé changes, then commit the new PDF.
- **Must not be served:** anything outside `public/`, including `resume/`, `docs/`, `plans/`, `PRODUCT.md`, and `README.md`.

### Files under `public/`

```text
index.html
styles.css
assets/favicon.svg
assets/resume-portfolio.pdf
assets/images/mailcart-composer.webp
assets/images/nu-insights-plan.webp
assets/images/auto-lead-demo.webp
assets/fonts/fraunces-latin-opsz.woff2
assets/fonts/sora-latin-wght.woff2
assets/fonts/public-sans-latin-wght.woff2
assets/fonts/Fraunces-OFL.txt
assets/fonts/PublicSans-OFL.txt
assets/fonts/Sora-OFL.txt
```

## Local preview (not production)

```sh
python3 -m http.server 8000 --directory public
```

This is a development preview only. **Production uses Railway Railpack's static-site provider and Caddy**, configured by `Staticfile` and `railway.json`. The Python command remains local-preview-only.

## Runtime requirements

- **Dependencies:** none. Any static file server works.
- **Content types the server must send:** `text/html`, `text/css`, `font/woff2`, `image/webp`, `image/svg+xml`, `application/pdf`.
- **Environment variables:** none. No secrets, API keys, or account credentials belong in this repository.
- **Port:** whatever Railway requires. The site has no port of its own.

## URL and path assumptions

- Single page at `/`. Every asset reference is relative (`styles.css`, `assets/...`), so the site works at a domain root.
- In-page anchors: `#main`, `#top`, `#projects`, `#background`, `#contact`. No other routes and no rewrites.
- `og:url` is set to `https://josephkelly.dev/`.
- There is no custom 404 page. The host's default is acceptable.

## Caching

- No asset filenames are fingerprinted. Keep `index.html` and `styles.css` on a short or revalidating cache, so updates appear without a cache purge.
- Fonts and images rarely change and can be cached longer. If an image or the PDF is replaced under the same name, purge the CDN cache.
- If Cloudflare proxying is enabled, check that it does not modify the PDF or fonts. Choose the proxy setting from current Railway and Cloudflare guidance.

## Domain and DNS

| Item | Value |
| --- | --- |
| Domain | `josephkelly.dev` (owned by Joseph) |
| Hosting | Railway (Joseph's existing subscription) |
| DNS | Cloudflare |
| Existing subdomain that must keep working | `nuinsights.josephkelly.dev` (NU Insights, a separate Railway service) |
| `www` alias | **Undecided.** Ask Joseph before adding records |

Preserve every unrelated DNS record, including NU Insights and any email records. Record the prior values of any record that changes.

## Repository state

- Branch `main`, remote `origin` = `https://github.com/joseph-kelly1/portfolio.git`.
- At handoff, `main` was level with `origin/main` at commit `7a9d2e9` ("Add project screenshots and downloadable resume").
- Stage 5 documentation edits (`docs/qa.md`, this file, `README.md`, `docs/decisions.md`) are uncommitted until Joseph commits them.
- `plans/` is ignored by Git and exists only locally.

## QA evidence and status

- Full results: `docs/qa.md`. Every check that was run passed; there are 0 axe violations and no console errors.
- **Not covered:** Safari, Firefox, real devices, the native mobile PDF viewer, and a screen reader. These are recommended spot checks once the site is on the custom domain.
- **Launch blockers:** none in the implementation.
- **Content approval:** the Stage 1 brief was approved on 2026-10-14. Stages 2–5 were implemented on Joseph's requests. **Joseph authorized deployment on 2026-10-14.**
- **Open content choices (non-blocking):** the NU Insights code link, the Khoury "Science"/"Sciences" wording, and a social preview image. See `docs/qa.md`.

## Post-deploy verification (same journey on the custom domain)

1. `https://josephkelly.dev/` returns 200 over a valid certificate.
2. Fonts, both images, and the favicon load. `assets/resume-portfolio.pdf` returns `application/pdf`.
3. GitHub, LinkedIn, MailCart, NU Insights, NU Insights code, and mailto links all work.
4. `https://nuinsights.josephkelly.dev` still serves NU Insights.
5. Deployed files contain no phone number. Re-run the scan in `docs/qa.md` against the deployed PDF if needed.
