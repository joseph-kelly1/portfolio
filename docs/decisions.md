# Decisions

## Stage status

| Stage | Status |
| --- | --- |
| 1. Content and design brief | Accepted by Joseph, 2026-10-14 |
| 2. Working page skeleton | Complete, 2026-10-14 |
| 3–6 | Not started |

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
| Repository links | Omitted; none supplied |
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

## Carried into later stages

- Stage 2: until the PDF exists, show "Résumé PDF pending" instead of a live résumé link.
- Stage 3: confirm the OFL license file ships with downloaded Fraunces and Public Sans files before committing them. Decide whether the project image/copy layout alternates.
- Stage 4: capture actual MailCart and NU Insights screenshots and export `public/assets/resume-portfolio.pdf` without a phone number.
- Stage 5: recheck that all supplied URLs resolve (all passed in Stage 2).
