# Joseph Kelly Portfolio

Static one-page portfolio. The public web root is `public/`. Everything in it is served as is, with no build step.

## Preview locally

```sh
python3 -m http.server 8000 --directory public
```

Then open http://localhost:8000.

## Layout

- `public/index.html`: page content (the authoritative copy of visible text)
- `public/styles.css`: styles and design tokens
- `public/assets/`: fonts, screenshots, favicon, public résumé PDF
- `docs/`: content brief, decisions, QA notes
- `resume/resume-portfolio.tex`: résumé source, kept outside the web root

## Public résumé PDF

`public/assets/resume-portfolio.pdf` is compiled from `resume/resume-portfolio.tex`. The source has no phone number; keep it that way. To rebuild with TeX Live:

```sh
mkdir -p /tmp/resume-build
pdflatex -interaction=nonstopmode -halt-on-error -output-directory=/tmp/resume-build \
  -jobname=resume-portfolio \
  "\PassOptionsToPackage{pdftitle={Joseph Kelly - Resume},pdfauthor={Joseph Kelly}}{hyperref}\input{resume/resume-portfolio.tex}"
# run it a second time so hyperref bookmarks settle, then:
cp /tmp/resume-build/resume-portfolio.pdf public/assets/resume-portfolio.pdf
```

The command sets the PDF title and author without editing the source. Before publishing, check that the PDF still has the email address and no phone number. For example, open it and search, or extract its text with any PDF tool.

## Assets

| File | Source | Rights |
| --- | --- | --- |
| `assets/fonts/fraunces-latin-opsz.woff2` | Fontsource `@fontsource-variable/fraunces` 5.3.0 (latin, wght + opsz) | SIL OFL 1.1, `Fraunces-OFL.txt` |
| `assets/fonts/public-sans-latin-wght.woff2` | Fontsource `@fontsource-variable/public-sans` 5.3.0 (latin, wght) | SIL OFL 1.1, `PublicSans-OFL.txt` |
| `assets/images/mailcart-composer.webp` | Composer preview on the public usemailcart.com home page; example contact data only | Joseph's product |
| `assets/images/nu-insights-plan.webp` | Course Builder on nuinsights.josephkelly.dev with an example plan (Computer Science, BACS, 2026–2027 catalog, Systems concentration, "Fill without AI") | Joseph's product |
| `assets/favicon.svg` | Hand-written "JK" monogram | Original |

### Replacing a screenshot

1. Capture the real interface at 2x device scale, showing example data only. Never include a personal inbox, private records, or a phone number.
2. Convert it to WebP about 1400px wide: `cwebp -q 82 -resize 1400 0 in.png -o public/assets/images/<name>.webp`.
3. Update the `<img>` `width`, `height`, and `alt` in `public/index.html`. Keep the first project image eager and later images `loading="lazy"`.
