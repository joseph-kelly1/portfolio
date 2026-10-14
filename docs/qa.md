# QA Report

Stage 5. Run 2026-10-14 against commit `7a9d2e9` on `main`, served locally with `python3 -m http.server 8000 --directory public` after a clean restart.

## Environment

- macOS (Darwin 25.6), Python 3.13.7.
- Browser: Playwright Chromium via `playwright-cli`. All browser checks ran in Chromium only.
- Accessibility scan: axe-core 4.10.2, injected from cdnjs into the test page only. The site does not load it.
- PDF checks: macOS PDFKit (text, links, metadata) and visual rendering.

## Results

Status values: **Pass** = run and passed. **Not run** = not performed (see Limitations).

| Area | Check | Result |
| --- | --- | --- |
| Serving | `/`, `styles.css`, both fonts, both images, favicon, and the PDF return 200 with the correct content type (`text/html`, `text/css`, `font/woff2`, `image/webp`, `image/svg+xml`, `application/pdf`) | Pass |
| Serving | `resume/resume-portfolio.tex` is not reachable (404; outside the web root) | Pass |
| Visitor journey | Intro, then professional links, both projects, background, and contact appear in the approved order. The résumé button opens the PDF | Pass |
| External links | GitHub profile, LinkedIn, usemailcart.com, nuinsights.josephkelly.dev, and github.com/joseph-kelly1/nu-insights return HTTP 200 with no redirects (curl) | Pass |
| Email | Every `mailto:` targets `kelly.jos@northeastern.edu` | Pass |
| Layout | No horizontal overflow at 320, 360, 390, 768, 1024, 1280, 1440, or 1920 px. Captures reviewed at 320, 390, 768, 1024, and 1440 | Pass |
| Zoom | Reflow at 640 px (200% of a 1280 window) and 320 px (400%): no overflow or clipped text | Pass (emulated) |
| Keyboard | Tab order: skip link → name → Projects → Background → Contact → View résumé → GitHub → LinkedIn → Email → Visit MailCart → Visit NU Insights → NU code → footer email → footer pills. Every stop shows a 3px outline | Pass |
| Keyboard | Skip link moves focus to `main`. Nav "Projects" scrolls the section to the top | Pass |
| Reduced motion | `reduce`: `scroll-behavior: auto`, transitions 0s. `no-preference`: smooth scroll, 160ms transitions | Pass |
| JavaScript disabled | All 17 links and both images render; the page uses no JavaScript | Pass |
| Font failure | With `.woff2` requests aborted, Georgia/system fallbacks render and nothing overflows at 320 px | Pass |
| Structure | `lang="en"`, one `h1`, h2 → h3 hierarchy, header/nav/main/footer landmarks, no duplicate ids | Pass |
| Accessibility scan | axe WCAG 2.0/2.1/2.2 A+AA plus best-practice: 0 violations, 0 incomplete, 37 passing rules | Pass |
| Contrast | Lowest text pair is 4.6:1 (white on `--action`). Full table in `plans/DESIGN.md` | Pass |
| Touch targets | Pills ≥ 48 px tall, nav and project links ≥ 44 px tall (measured at 390 px, mobile emulation) | Pass |
| Images | Declared `width`/`height` match the intrinsic sizes (1400×1077, 1400×784). Descriptive alt text. Second image lazy. No EXIF/XMP data | Pass |
| Metadata | Title, description, `og:type`/`og:title`/`og:description`/`og:url`, `twitter:card=summary`, SVG favicon | Pass |
| Console | No console errors or warnings, and no page errors | Pass |
| Network | No 4xx/5xx responses. Chromium logged one `requestfailed` for the favicon while the server recorded 200 for all nine favicon requests; this is a cancelled duplicate fetch, not a missing file | Pass |
| Performance | Total transfer 187 KB: HTML 6.8, CSS 8.1, Fraunces 65.7, Public Sans 26.2, images 45.5 + 34.8, favicon 0.2. CLS 0. LCP element is the `h1` (48 ms on localhost) | Pass |
| Copy | Visible text proofread against `docs/content.md`; no stale "pending" or placeholder text remains | Pass |
| Résumé PDF | One page, readable. Extracted text contains the email. Links are mailto, LinkedIn, MailCart, and NU Insights. Metadata holds title/author/producer only. Mobile-emulated request returns 200 `application/pdf` with a `%PDF-` header | Pass |
| Privacy | No phone-like pattern in the PDF text, any file under `public/`, or any tracked file. Both screenshots visually show example data only. The `.tex` source is unchanged (SHA-1 `f5b8e622…`) | Pass |

## Fixes in this stage

None were needed: no defects were found.

## Content notes for Joseph (not defects)

- "Khoury College of Computer Science" matches the résumé. The college's official name is "Khoury College of Computer Sciences". Change both together if wanted.
- The NU Insights code link was added in Stage 4 from a verified public repository. Remove it if a code link is not wanted.
- No social preview image (`og:image`). Shared links show only the title and description.
- At about 960–1100 px the project screenshots sit in a narrower column. They stay legible as illustrations, but their small UI text is not readable at that size.

## Limitations (not run)

- Safari, Firefox, and real iOS/Android devices were not tested. The phone PDF experience was checked only through a mobile-emulated Chromium request, not the native PDF viewer.
- Real browser zoom was emulated by reducing the CSS viewport width.
- No screen reader pass (VoiceOver/NVDA).
- No Lighthouse or remote performance test. Timings are localhost-only and say nothing about production latency.
- LinkedIn returns 200 to curl, but its content for signed-out visitors was not inspected.

## Subsequent UI wording change

Joseph requested regular e characters in the resume labels. Updated the intro action to “View resume (PDF)”, the footer link to “Resume (PDF)”, and the page/social descriptions to plain “resume”. Refreshed the localhost browser and confirmed both link labels. Both links still target `assets/resume-portfolio.pdf`; the PDF itself is unchanged. This was a copy-only change, not a repeat of the complete Stage 5 QA run.

Stage 6 is deferred while Joseph makes UI changes. Recheck affected areas before any eventual deployment.

## Subsequent typography change

Replaced the decorative serif with Public Sans for headings, the site name, and the role line at Joseph's request. Refreshed localhost and visually checked the revised title. Computed styles confirm Public Sans for both the main heading and site name; no horizontal overflow occurs at the current browser width. Fraunces is no longer declared or preloaded. This is a targeted check of the font change, not a repeat of the complete Stage 5 QA run.

## Selected Sora typography

Joseph selected Sora from the comparison. The site now self-hosts Sora 500 for headings, site name, and role line, while retaining Public Sans for body text. Its variable WOFF2 is from `@fontsource-variable/sora` 5.3.0, downloaded with package integrity checked and its OFL license retained.

Refreshed localhost and visually checked the heading. Computed styles confirm Sora 500 for the main heading and Public Sans for the body. No horizontal overflow at 320, 390, or 1440 pixels; temporary viewport overrides were reset afterward. The complete Stage 5 QA suite was not repeated. Hosting remains deferred.
