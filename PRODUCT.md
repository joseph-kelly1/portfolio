# Product Context: Joseph Kelly Portfolio

Approved by Joseph, 2026-10-14 (Stage 1).

## Purpose

A one-page personal portfolio. It helps recruiters and hiring managers quickly understand Joseph's focus, inspect two substantive projects, and reach his GitHub, LinkedIn, and school email without hunting through navigation.

## Audience

Recruiters and hiring managers. They usually read on a laptop during the workday and may revisit on a phone. They scan quickly and decide within seconds whether to open a project.

## Personality

Clean, confident, understated. Concrete, first-person copy in Joseph's voice. The work, shown in actual screenshots, carries the visual interest.

## Content

Content lives in `docs/content.md`. Section order:

1. Introduction
2. Professional links: GitHub, LinkedIn, school email
3. MailCart
4. NU Insights
5. Compact background: education and experience
6. Contact footer

## Anti-references

- Generic developer-portfolio templates: dark terminal themes, skill-bar charts, walls of identical cards.
- Decorative motion: parallax, cursor effects, autoplay, typewriter intros.
- Gradient text, glass surfaces, hamburger menus for a single page.
- Inflated claims, slogans, invented metrics, testimonials, or availability statements.
- Any reference brand name in copy, metadata, or assets.

## Accessibility

- WCAG AA contrast for every text/background pair actually used.
- Semantic landmarks, a skip link, one `h1`, and logical headings.
- Full keyboard access with visible focus, and touch targets of at least 44×44 px.
- Honor `prefers-reduced-motion`; never hide content until JavaScript runs.
- All content and links work with JavaScript disabled.
- No horizontal scroll at 320 px; text holds up under zoom.

## Privacy

Only the school email is public. Keep the personal email and résumé PDF off the site. The phone number must never appear in source, metadata, screenshots, or other public assets. The original résumé outside this repository stays unchanged.

## Execution policy

When Joseph requests implementation of a stage, begin that stage directly using the existing brief. Do not require another plan or design confirmation before doing the requested work. Plan internally as needed, implement and verify the stage, then report completion. Stop at the requested scope boundary so Joseph can choose the next stage.

## Technical constraints

Static HTML and CSS, with JavaScript only for a specific approved need. No framework, backend, database, CMS, auth, contact form, or analytics in the initial version. Hosting (Railway) and DNS (Cloudflare) are handled only in Stage 6.
