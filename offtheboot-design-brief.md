# OffTheBoot — Design Brief for Claude Code
**Version 1.0 · April 2026 · Paste at the start of every development session**

---

## Who is OffTheBoot

OffTheBoot is an online slow travel planning service for Northeast Italy — Veneto, Dolomiti, Friuli Venezia Giulia. Founded by Cesare and Alice, two Italians who left Italy for a decade (50+ countries, 10 years), then came back with fresh eyes and built a service to show international travellers the real Italy — the one most Italians themselves overlook.

The tagline that captures the brand perfectly: *"Italy is one of the most visited countries in the world, and one of the least discovered. We're here to change that."*

**Target customer:** International anglophone travellers (UK, US, DE, AU) who are sceptical of mass tourism, want authentic local experiences, and prefer slow travel without a car.

**What makes OffTheBoot different:**
- Human-led, locally grounded — not aggregated or algorithmic
- 100% car-free itineraries — every route works by train, bus or foot
- Local-first — every recommendation keeps money in local communities
- Real founders with a real story — not a corporate travel agency

**Brand values (in order of importance):**
1. Respect for nature, local communities and traditions
2. Genuine human connections
3. Curiosity and open-mindedness

---

## The design system

OffTheBoot uses a fully defined design system. All tokens are in `globals.css`. **Never hardcode any colour, font, or spacing value — always use CSS variables.**

### Colours

| Variable | Hex | Use |
|---|---|---|
| `--color-primary` | `#2E5855` | Navbar bg, primary buttons, structural elements |
| `--color-accent` | `#C4920A` | Price/duration badge backgrounds ONLY |
| `--color-cta` | `#D4701A` | CTA buttons ONLY — one per section maximum |
| `--color-ink` | `#1E1C16` | All text, dark section backgrounds, footer |
| `--color-parchment` | `#EDE5D0` | Tagline strip, alternate surfaces |
| `--color-bg` | `#FAFAF4` | Page background — NEVER use pure `#ffffff` |
| `--color-muted` | `#6B6457` | Secondary text, meta, placeholders |
| `--color-yellow-wheat` | `#F5E8A8` | Itinerary section backgrounds |
| `--color-yellow-butter` | `#FDF5CC` | Newsletter section background |
| `--color-green-sage` | `#D8ECD8` | Values/features section background |
| `--color-green-mist` | `#EAF3EC` | Category badge backgrounds |

**Critical colour rules:**
- `--color-accent` (Stone Gold) MUST NEVER be used as text on white — fails WCAG (2.4:1 contrast)
- `--color-cta` (Terracotta) maximum ONE per section — never stack multiple CTA-coloured elements
- Background colours (`--color-bg`) must be `#FAFAF4` not `#ffffff` — pure white feels like a SaaS app
- Tint colours (yellow, green variants) are for backgrounds only — never use as text colour

**Page colour rhythm** — alternate sections to create breathing:
1. Ink dark (hero)
2. Parchment strip (tagline)
3. Warm White (itineraries)
4. Warm White (who we are)
5. Sage Green (values strip)
6. Ink dark (testimonials)
7. Warm White (blog)
8. Ink dark (CTA)
9. Yellow Wheat (newsletter)
10. Ink dark (footer)

Avoid two consecutive sections with the same background colour.

### Typography

**Three fonts. Never introduce a fourth.** Fraunces is logo-only — never use it for headings, body, or UI.

| Variable | Value | Use |
|---|---|---|
| `--font-display` | `'Young Serif', Georgia, serif` | All headings, card titles, stat numbers |
| `--font-body` | `'Lora', Georgia, serif` | Body text, nav, buttons, labels, badges (italic available) |
| `--font-logo` | `'Fraunces', Georgia, serif` | Logo wordmark ONLY (navbar + footer) — applied via `.logo-wordmark` utility: weight 900, `font-optical-sizing: auto`, `font-variation-settings: 'SOFT' 94.9, 'WONK' 1` |

**Young Serif rules:**
- Single weight 400 only — there is no bold variant
- Visual weight comes from SIZE and TRACKING, not font weight
- Negative tracking on large text: `letter-spacing: -0.02em` at 40px+
- Use italic (`font-style: italic`) for pull quotes, testimonials, H3 accents
- NEVER use for body text, buttons, labels, or nav links

**Lora rules:**
- Available weights: 400, 500, 600, 700 — italics available at every weight
- Lora has no weight 300; use 400 as the lightest weight (body)
- Weight 400 for body text, descriptions, and nav links
- Weight 500 for card metadata and secondary UI
- Weight 600 for button labels and CTA links
- Weight 700 for badges, eyebrows, and overlines
- Use italic for inline emphasis, pull-quote attributions, and editorial accents
- NEVER use for page headings or section titles

**Fraunces rules:**
- Logo wordmark ONLY — never for headings, body, or UI
- Always applied via the `.logo-wordmark` utility class (handles weight + variation axes)
- Loaded with axes `opsz`, `SOFT`, `WONK` — locked to weight 900, SOFT 94.9, WONK 1
- Used in the brand wordmark in navbar and footer; nothing else

**Type scale:**
```css
--text-hero:   4rem      /* 64px */
--text-h1:     2.5rem    /* 40px */
--text-h2:     1.75rem   /* 28px */
--text-h3:     1.25rem   /* 20px — italic, Forest Teal */
--text-body:   1rem      /* 16px — Lora 400 (bumped to 17px on ≥900px screens) */
--text-ui:     0.875rem  /* 14px — Lora 400/500 */
--text-label:  0.75rem   /* 12px — Lora 600, uppercase */
--text-xs:     0.625rem  /* 10px — Lora 700, uppercase, wide tracking */
```

**Eyebrow / overline pattern** — used before every section title:
```css
font-family: var(--font-body);
font-size: var(--text-xs);
font-weight: 700;
letter-spacing: 0.18em;
text-transform: uppercase;
color: var(--color-muted);
```
Always add a short horizontal line before the text using `::before` with `width: 20px; height: 1px; background: currentColor`.

### Google Fonts import

In the Next.js site, fonts are loaded via `next/font/google` in `app/layout.tsx` — never link to the Google Fonts CDN from `globals.css`. For static reference pages (the design-system showcase HTML), use:
```html
<link href="https://fonts.googleapis.com/css2?family=Young+Serif&family=Lora:ital,wght@0,400..700;1,400..700&family=Fraunces:opsz,wght,SOFT,WONK@9..144,900,94.9,1&display=swap" rel="stylesheet">
```

### Badge system

Two badge types only:
```html
<!-- Category / style badges -->
<span class="badge-category">Slow travel</span>
<!-- bg: --color-green-mist · text: --color-primary -->

<!-- Price / duration badges -->
<span class="badge-price">€1.200</span>
<!-- bg: --color-accent · text: --color-ink -->
```
Never mix the two types on the same element. Never use more than 2–3 badges per card.

---

## Tech stack

```
Framework:  Next.js 16 (App Router)
Language:   TypeScript
Styling:    Tailwind CSS v4 (with CSS variables from globals.css)
CMS:        Sanity (content managed via Sanity Studio at /studio)
Hosting:    Vercel (auto-deploy from GitHub main branch)
Forms:      Tally (embedded iframe for /plan-your-trip)
Fonts:      next/font/google — Young Serif + Lora + Fraunces (logo only)
```

**Tailwind + CSS variables:** Use Tailwind utility classes where possible. For design system values (colours, fonts), use the CSS variables via Tailwind's arbitrary value syntax: `bg-[var(--color-primary)]`, `text-[var(--color-ink)]`, `font-[var(--font-display)]`. Or extend `tailwind.config.ts` with the token mapping included in `globals.css`.

**Sanity integration:** All content-driven sections (itinerary cards, blog posts, services) pull data from Sanity. Static copy (hero headline, value propositions, about text) can be hardcoded or managed via Sanity singletons. The CMS schema is already set up.

---

## Page structure

| Page | Path | Status |
|---|---|---|
| Homepage | `/` | Build first |
| Services | `/services` | Build second |
| Plan your trip | `/plan-your-trip` | Tally form embed |
| Blog listing | `/blog` | Planned |
| Blog post | `/blog/[slug]` | Planned |
| About | `/about` | Planned |
| Privacy Policy | `/privacy-policy` | Required — GDPR |
| Terms | `/terms` | Required |
| Thank You | `/thank-you` | After Tally form |

---

## Component build order

Build in this order — do not skip ahead. Each step depends on the previous.

### Phase 1 — Foundation
1. `globals.css` — paste tokens, base styles, utility classes
2. `layout.tsx` — font import, metadata, navbar, footer
3. `Navbar` component — floating white pill that docks to a full-width bar on scroll; logo via `.logo-wordmark` (Fraunces), links Lora 600 uppercase, terracotta pill CTA
4. `Footer` component — Ink bg, 4-column grid, logo, links

### Phase 2 — Homepage sections
5. `HeroSection` — Ink dark bg, large Young Serif title, stats row, card grid on right
6. `TaglineStrip` — Parchment bg, italic Young Serif centered quote
7. `ItinerariesSection` — Warm White, 3-col card grid pulling from Sanity
8. `ItineraryCard` — image, type badge, title, description, badge row, price
9. `WhoWeAreSection` — Warm White, 2-col, founders story + values list
10. `ValuesStrip` — Sage Green bg, 3-col grid with border-left teal
11. `TestimonialsSection` — Ink dark bg, 3-col quote cards
12. `BlogSection` — Warm White, featured post + list sidebar
13. `CtaSection` — Ink dark bg, 3-step process + CTA button
14. `NewsletterSection` — Yellow Wheat bg, email form

### Phase 3 — Inner pages
15. `/services` — Sanity-driven service cards
16. `/plan-your-trip` — Tally form embed
17. `/blog` — listing page with Sanity data
18. `/blog/[slug]` — post page

### Phase 4 — Legal & utility
19. `/privacy-policy` — static content page
20. `/terms` — static content page
21. `/thank-you` — post-form confirmation

---

## Writing tone — copy guidelines

When writing placeholder or real copy for the site:

- **Voice:** Warm, direct, personal. Written by a human, not a marketing team.
- **No:** "Discover amazing experiences", "Unforgettable adventures", "Best-in-class service"
- **Yes:** "Away from the crowds", "The Italy most Italians overlook", "Real local knowledge"
- **CTAs:** Always action-first — "Plan your trip", "See itineraries", "Read the story"
- **Never mention** "sustainability" directly — use "slow", "local", "community", "human", "ethical"
- All copy is in **English only** — even if you see Italian names or places

---

## WCAG accessibility requirements

All components must meet these minimum contrast ratios:
- Body text on background: minimum 7:1 (AAA)
- UI text on coloured bg: minimum 4.5:1 (AA)
- CTA button (`--color-cta` on white): 4.6:1 — passes AA
- Never place `--color-accent` as text on white — 2.4:1 fails

Interactive elements must be identifiable by shape and label, not colour alone.

---

## Quick reference — what to do if unsure

| Question | Answer |
|---|---|
| Which background for a new section? | Warm White (`--color-bg`) — unless it follows another Warm White section |
| Which font for a heading? | Young Serif (`--font-display`) |
| Which font for a paragraph? | Lora (`--font-body`, weight 400 — Lora has no 300) |
| Which font for the logo? | Fraunces, via `.logo-wordmark` utility — never anywhere else |
| Which colour for a button? | CTA buttons → `--color-cta`. All other buttons → `--color-primary` or outlined |
| Can I add a new colour? | No. Use the existing palette. If something feels missing, ask first |
| Can I use pure white `#fff`? | No. Always `var(--color-bg)` which is `#FAFAF4` |
| What tracking for big titles? | `letter-spacing: -0.02em` at 40px+, `-0.01em` at 28px |
| What tracking for uppercase labels? | `letter-spacing: 0.16em` minimum |
