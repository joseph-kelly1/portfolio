# Portfolio Content Brief

Status: **Approved by Joseph on 2026-10-14 (Stage 1).** Copy below is the established brief. When Joseph requests an implementation stage or revision, carry out that work directly using this copy; do not add a separate plan-confirmation round. Preserve factual claims and the agreed direction.

Source of facts: `resume/resume-portfolio.tex` and `plans/PLAN.md`. Links below are supplied, not yet checked; they are validated in Stage 2 and Stage 5.

Once implemented, the HTML is the single authoritative copy of visible content. This file is the editorial brief behind it.

## Page title and metadata

- Page title: `Joseph Kelly — Software Portfolio`
- Meta description: "Joseph Kelly is a computer science student at Northeastern University building full-stack software. Projects, resume, and contact."

## 1. Introduction

- Heading: **Joseph Kelly**
- Role line: "Computer science student building full-stack software."
- Bio: "I study computer science at Northeastern University with a concentration in systems. I build products end to end, from schedulers and data pipelines to billing and email delivery, and I'm currently a Technical Operations & Automation Co-op at SLATE."

## 2. Professional links (directly under the introduction)

| Label | Destination | Treatment |
| --- | --- | --- |
| View resume (PDF) | `assets/resume-portfolio.pdf` | Primary action |
| GitHub | https://github.com/joseph-kelly1 | Secondary |
| LinkedIn | https://linkedin.com/in/joseph-kelly4/ | Secondary |
| Email | mailto:kelly.jos@northeastern.edu | Secondary |

## 3. Selected projects

Order: MailCart, then NU Insights.

### MailCart

- Live site: https://usemailcart.com
- Repository: none public; no link shown
- Role: Founder & Full-Stack Developer · Mar 2026 – present
- Problem: "Personalized outreach usually means copying and pasting the same message into dozens of emails. MailCart turns a spreadsheet into individually personalized emails sent from your own Gmail or Outlook mailbox."
- Contributions:
  - Built asynchronous per-recipient sending with spreadsheet-driven personalization, conditional content, attachments, and live progress, with cancellation and retry handling.
  - Integrated the Gmail and Microsoft Graph APIs, Clerk authentication, and Stripe subscriptions with team-seat billing.
  - Kept UI previews and sent messages consistent with shared cross-language personalization tests, part of a 495-test suite.
- Technologies: React, FastAPI, PostgreSQL, Stripe, Clerk, OpenAI API
- Screenshot: composer with live preview from the public home page, example contact data (`assets/images/mailcart-composer.webp`)

### NU Insights

- Live site: https://nuinsights.josephkelly.dev
- Repository: https://github.com/joseph-kelly1/nu-insights (public; found under Joseph's GitHub account in Stage 4, and its README links the live app)
- Role: Creator & Developer · Jan 2026 – present
- Problem: "Planning a Northeastern degree means juggling prerequisites, credit limits, co-op terms, and changing catalog requirements. NU Insights builds a semester-by-semester plan that satisfies them."
- Contributions:
  - Built a constraint-based semester planner with OR-Tools CP-SAT that enforces prerequisites, corequisites, credit limits, and degree requirements while respecting completed courses, pinned courses, and co-op terms.
  - Scraped 6,034 courses and requirements for 395 program variants, including archived catalog editions for year-specific planning.
  - Added catalog-grounded AI explanations and elective ranking across multiple LLM providers, with a deterministic fallback when a response fails.
- Technologies: React, Flask, SQLite, OR-Tools, Docker, Railway
- Screenshot: Course Builder first year of an example plan generated without AI (`assets/images/nu-insights-plan.webp`)

## 4. Background (compact)

**Education**
Northeastern University, Khoury College of Computer Science — B.S. in Computer Science, Systems Concentration, Minor in Mathematics. Expected May 2028.
GPA is not shown on the page; the resume carries it.

**Experience**
- SLATE — Technical Operations & Automation Co-op · Jul 2026 – present
  "Building Python QA and document-analysis tools for healthcare claims and plan contracts."
- Alactive, London — Mobile Frontend Engineer · Nov 2024 – Dec 2024
  "Shipped SwiftUI features for an early-stage iOS app."

Leadership and coursework are omitted; the resume carries them.

## 5. Footer / contact

- Line: "Get in touch: kelly.jos@northeastern.edu"
- Repeat links: Email, GitHub, LinkedIn, Resume
- No phone number anywhere.

## Wireframes

### Desktop (~1440px)

```text
+--------------------------------------------------------------------+
| Joseph Kelly                          Projects  Background  Contact |
+--------------------------------------------------------------------+
|                                                                    |
|  JOSEPH KELLY                       (serif display)                |
|  Computer science student building full-stack software.            |
|  Bio, two sentences, max ~70ch                                     |
|                                                                    |
|  ( View resume )   GitHub   LinkedIn   Email                       |
|                                                                    |
|---------------------------------------------- hairline ------------|
|  Selected projects                                                 |
|                                                                    |
|  MailCart                        +------------------------------+  |
|  Founder & Full-Stack Developer  |                              |  |
|  Problem, 2 sentences            |   MailCart screenshot        |  |
|  - contribution                  |   (soft 24px frame)          |  |
|  - contribution                  |                              |  |
|  - contribution                  +------------------------------+  |
|  React · FastAPI · PostgreSQL ...                                  |
|  Visit site ->                                                     |
|                                                                    |
|  +------------------------------+  NU Insights                     |
|  |                              |  Role                            |
|  |   NU Insights screenshot     |  Problem, 2 sentences            |
|  |                              |  - contribution x3               |
|  +------------------------------+  React · Flask · OR-Tools ...    |
|                                    Visit site ->                   |
|---------------------------------------------- hairline ------------|
|  Background                                                        |
|  Education                    |  Experience                        |
|  Northeastern, B.S. CS ...    |  SLATE — Co-op                     |
|                               |  Alactive — Mobile Frontend        |
+--------------------------------------------------------------------+
| kelly.jos@northeastern.edu      Email  GitHub  LinkedIn  Resume    |
+--------------------------------------------------------------------+
```

Image/copy alternation on the second project is optional; decide in Stage 3.

### Mobile (~390px)

```text
+--------------------------+
| Joseph Kelly             |
| Projects Background      |
| Contact                  |
+--------------------------+
| JOSEPH KELLY             |
| Computer science student |
| building full-stack      |
| software.                |
| Bio ...                  |
|                          |
| ( View resume )          |
| GitHub  LinkedIn  Email  |
|--------------------------|
| Selected projects        |
| MailCart                 |
| Role                     |
| +----------------------+ |
| |  screenshot (16px)   | |
| +----------------------+ |
| Problem                  |
| - contributions          |
| Tech list                |
| Visit site ->            |
|                          |
| NU Insights (same order) |
|--------------------------|
| Background               |
| Education                |
| Experience               |
|--------------------------|
| Email                    |
| GitHub LinkedIn Resume   |
+--------------------------+
```

Mobile order inside each project: title, role, screenshot, problem, contributions, technologies, links. Professional links wrap; nothing scrolls horizontally.

## Visual choices for review

**Direction (approved):** `plans/DESIGN.md` as written: warm paper, serif headings, sans body, one blue action, real screenshots.

**Fonts** (all SIL Open Font License 1.1, self-hostable; confirm the license file ships with the downloaded files before committing them in Stage 3):

| Option | Headings | Body | Character |
| --- | --- | --- | --- |
| A (approved) | Fraunces, light–regular, optical size on | Public Sans 400/600 | Warm, slightly expressive serif; neutral sans |
| B (not chosen) | Newsreader, regular | Public Sans 400/600 | Quieter, more editorial |

Fallbacks: `Georgia, serif` for headings, `system-ui, sans-serif` for body.

**Primary action (approved):** "View resume" as a blue pill button with white text. Contrast note: white text on `#2a72de` is about 4.6:1 (passes AA). Canvas-colored text (`#f7f1e8`) on that blue is about 4.1:1 and fails for normal-size text, so the button needs white text or a slightly darker blue.
