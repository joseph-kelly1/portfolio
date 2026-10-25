# Joseph Kelly Portfolio

Static one-page portfolio. The public web root is `public/`. Everything in it is served as is, with no build step.

## Preview locally

```sh
python3 -m http.server 8000 --directory public
```

Then open http://localhost:8000.

This is a development preview, not production hosting. There is no build step and there are no dependencies or environment variables. Deployment notes are in `docs/deployment-handoff.md` and QA evidence is in `docs/qa.md`.

## Layout

- `public/index.html`: page content (the authoritative copy of visible text)
- `public/styles.css`: styles and design tokens
- `public/assets/`: fonts, screenshots, favicon
- `docs/`: content brief (`content.md`), decisions, QA report (`qa.md`), deployment handoff
- `resume/resume-portfolio.tex`: résumé source, kept outside the web root

## Privacy

The résumé PDF and personal email are not published. Keep the résumé source outside `public/`; only the school email is shown for contact.

## Assets

| File | Source | Rights |
| --- | --- | --- |
| `assets/fonts/fraunces-latin-opsz.woff2` | Fontsource `@fontsource-variable/fraunces` 5.3.0 (latin, wght + opsz); retained but no longer loaded | SIL OFL 1.1, `Fraunces-OFL.txt` |
| `assets/fonts/sora-latin-wght.woff2` | Fontsource `@fontsource-variable/sora` 5.3.0 (latin, wght), headings/name/role | SIL OFL 1.1, `Sora-OFL.txt` |
| `assets/fonts/public-sans-latin-wght.woff2` | Fontsource `@fontsource-variable/public-sans` 5.3.0 (latin, wght) | SIL OFL 1.1, `PublicSans-OFL.txt` |
| `assets/images/mailcart-composer.webp` | Composer preview on the public usemailcart.com home page; example contact data only | Joseph's product |
| `assets/images/nu-insights-plan.webp` | Course Builder on nuinsights.josephkelly.dev with an example plan (Computer Science, BACS, 2026–2027 catalog, Systems concentration, "Fill without AI") | Joseph's product |
| `assets/images/auto-lead-demo.webp` | `docs/assets/demo.png` in github.com/joseph-kelly1/auto-lead (synthetic demo, fictional parcels) | Joseph's project |
| `assets/favicon.svg` | Hand-written "JK" monogram | Original |

### Replacing a screenshot

1. Capture the real interface at 2x device scale, showing example data only. Never include a personal inbox, private records, or a phone number.
2. Convert it to WebP about 1400px wide: `cwebp -q 82 -resize 1400 0 in.png -o public/assets/images/<name>.webp`.
3. Update the `<img>` `width`, `height`, and `alt` in `public/index.html`. Keep the first project image eager and later images `loading="lazy"`.

## Production hosting

Railway uses Railpack's static-site provider and Caddy. `Staticfile` explicitly limits the web root to `public/` and disables fallback routing, so missing paths return 404. Railpack, the HTTP healthcheck at `/`, and restart settings are configured on the Railway service.

There is no application build step. Screenshots, fonts, and licenses are included in Git. Keep private source files and planning documents outside `public/`.

Live site: https://josephkelly.dev/. GitHub pushes to `main` automatically deploy the linked Railway service. Service identifiers, DNS mapping, update steps, and rollback instructions are in `docs/deployment-handoff.md`.
