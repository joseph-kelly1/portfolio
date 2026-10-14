# Decisions

## Stage status

| Stage | Status |
| --- | --- |
| 1. Content and design brief | Accepted by Joseph, 2026-10-14 |
| 2. Working page skeleton | Complete, 2026-10-14 |
| 3. Visual styling | Complete, 2026-10-14 |
| 4. Projects and public résumé | Complete, 2026-10-14 |
| 5. QA and deployment handoff | Complete, 2026-10-14; awaiting Joseph's final acceptance |
| 6. Railway and Cloudflare release | In progress; Joseph authorized deployment, 2026-10-14 |

## Execution policy

Joseph's request to implement a stage is sufficient authorization to start. Do not pause after preparing a plan, require another brief approval, or ask for permission to implement the requested scope. Plan internally, implement, verify, and report completion. End after the requested stage or stage range so Joseph can choose what comes next; no formal acceptance phrase is required.

Localhost preview begins in Stage 2. Stage 3 adds the full visual treatment, and Stage 4 finishes screenshots and the public résumé PDF.

## Stage 1 decisions (approved 2026-10-14)

| Decision | Outcome |
| --- | --- |
| Headline / role line | "Computer science student building full-stack software." |
| Bio | As written in `docs/content.md` §1 |
| Project order | MailCart, then NU Insights |
| NU Insights role title | "Creator & Developer" |
| Repository links | MailCart: none public, omitted. NU Insights: `github.com/joseph-kelly1/nu-insights`, verified in Stage 4 |
| Background scope | Education + SLATE and Alactive lines only; no coursework |
| GPA on page | Not shown |
| Leadership section | Omitted |
| Visual direction | `plans/DESIGN.md` as written |
| Fonts | Fraunces (headings) + Public Sans (body), SIL OFL 1.1, self-hosted; fallbacks `Georgia, serif` / `system-ui, sans-serif` |
| Primary action | "View résumé", blue pill, white text (≈4.6:1 on `#2a72de`) |

## Stage 2 implementation decisions

| Decision | Outcome |
| --- | --- |
| Files | `public/index.html` and `public/styles.css`; no JavaScript |
| Preview | `python3 -m http.server 8000 --directory public` (see `README.md`) |
| Résumé | Plain "Résumé PDF pending" text, not a link, in the intro and footer |
| Screenshots | Dashed boxes labeled "Screenshot pending (Stage 4)" |
| Fonts | System fallbacks only; Fraunces and Public Sans arrive in Stage 3 |
| Contact | Footer carries `id="contact"`, and the nav links to it |

Verified 2026-10-14:
- Page and CSS return HTTP 200 locally.
- GitHub, LinkedIn, usemailcart.com, and nuinsights.josephkelly.dev return 200.
- No horizontal overflow at 320, 390, 768, or 1440 px.
- The skip link is the first focus stop and moves focus to `main`.
- The page has one `h1`.
- No phone number in `public/`.

## Stage 3 implementation decisions

| Decision | Outcome |
| --- | --- |
| Fonts | Fraunces (latin, wght + opsz axes, 67 KB) and Public Sans (latin, wght, 27 KB) from Fontsource 5.3.0; OFL texts in `public/assets/fonts/`; both preloaded |
| Tokens | OKLCH custom properties; full table in `plans/DESIGN.md` → Implemented system |
| Project layout | 5:7 copy/screenshot grid at ≥60rem, alternating sides; stacked below |
| Background layout | Two columns at ≥48rem |
| Footer | Dark `--night` surface (optional DESIGN.md role, now used) |
| Professional links | Outline pills; résumé stays a dashed "pending" pill until Stage 4 swaps in `.button-primary` |
| Motion | Color transitions and smooth scroll only, disabled under reduced motion |
| Unused palette | Olive, clay, ochre not used |

Verified 2026-10-14 in Chromium (playwright-cli):
- No horizontal overflow at 320, 390, 768, 1100, or 1440 px, or at 640 px (200% zoom of a 1280 px window).
- Layout holds at 320 px with the font files blocked.
- Every link and pill outside running text is at least 44 px tall.
- The focus ring is visible on pills, and the primary pill renders as white on `--action`.
- Contrast pairs are listed in DESIGN.md; the lowest text pair is 4.6:1.
- Not tested: Safari/Firefox, real touch devices, and real browser zoom (emulated by viewport width).

## Stage 4 implementation decisions

| Decision | Outcome |
| --- | --- |
| Project copy | Stage 1 copy kept unchanged; metrics limited to the approved "495-test suite", "6,034 courses", and "395 program variants" |
| NU Insights repo | Added "View NU Insights code on GitHub". The public repo is under Joseph's account and its README links the live app. Revisable if Joseph prefers no code link |
| MailCart screenshot | The app is behind sign-in, so the screenshot is the composer and live preview on the public home page (example contact "Emily Carter", example.com). Captured at 2x, 1400×1077 WebP, 47 KB, eager-loaded |
| NU Insights screenshot | Live Course Builder: CS BACS, 2026–2027 catalog, Systems concentration, "Fill without AI", first year cropped. 1400×784 WebP, 36 KB, `loading="lazy"` |
| Résumé | `assets/resume-portfolio.pdf` compiled from the unchanged `.tex` with pdfLaTeX; PDF title and author set at compile time. Intro: blue "View résumé (PDF)". Footer: "Résumé (PDF)" pill. Same-tab link, so the browser's PDF viewer opens it |
| Favicon | SVG "JK" monogram, ink on canvas |
| Social preview | `og:title`, `og:description`, `og:url`, and a `summary` card. No `og:image`, since no approved preview image exists |
| Placeholders | All removed (`.pending` and `.shot-placeholder` CSS deleted) |

Verified 2026-10-14:
- PDF: one page, readable. Text extracted with PDFKit contains `kelly.jos@northeastern.edu`, and no phone-like pattern appears in the text or the raw file. Its links are mailto, LinkedIn, usemailcart.com, and nuinsights.josephkelly.dev. Metadata holds title, author, and pdfTeX producer only.
- Local server returns 200 with the correct content type for the HTML, PDF, WebP, and SVG files. The nu-insights repo returns 200.
- No horizontal overflow at 320, 390, 768, 1100, or 1440 px.
- Both images load with their declared dimensions and alt text.
- "View résumé (PDF)" is the sixth Tab stop, after the skip link, name, and nav.
- `public/` contains no `.tex` file and no phone-like strings. The `.tex` source is unchanged (SHA-1 `f5b8e622…`).

## Stage 5 outcome

- QA was run in Chromium; every check that was run passed. No code changes were needed. Evidence and limitations: `docs/qa.md`.
- Handoff for Codex: `docs/deployment-handoff.md`. Serve `public/` with no build step; there are no environment variables; the PDF is committed.
- Open, non-blocking content choices: the NU Insights code link, the Khoury "Science"/"Sciences" wording, and an `og:image`.

## Carried into later stages

- Stage 6: after deploy, spot-check Safari, a real phone (including the PDF), and the custom-domain journey (`docs/deployment-handoff.md`). Decide on a `www` alias.

## Current UI revisions

- Use plain “resume” / “Resume” in site labels and metadata, with regular unaccented e characters, as requested by Joseph.
- Joseph authorized Stage 6 after completing UI changes on 2026-10-14, including publishing both email addresses and the current project updates.

- Hero: the role line and bio are replaced by two lines, "Computer Science at Northeastern" and "Technical Operations & Automation Co-op at SLATE", as separate `.role` paragraphs with a 0.5rem gap so they stay distinct when wrapped on phones.
- Projects: Auto Lead added as the third project, with copy drawn only from the public repo README. It has a GitHub link and no live link. The screenshot is the README's `docs/assets/demo.png` (synthetic data, 1280×720, converted to a 66 KB WebP, lazy). The meta line "Personal project" is Claude's wording because the README states no role; Joseph may rename it. Verified: no overflow at 320, 390, 768, or 1440 px, and axe reports 0 violations.
- Contact: personal email `josephkelly1107@gmail.com` added beside the school address in the footer "Get in touch" line. The "Email" pills still point to the school address.
- Typography: Joseph selected Sora after comparing alternatives. Use Sora 500 for headings, site name, and role line, with Public Sans for body text and controls. Sora is self-hosted from Fontsource 5.3.0, with its OFL license beside the font. Fraunces is retained as an unused asset and is not declared or preloaded.
