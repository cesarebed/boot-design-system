# OffTheBoot — Design Brief for Claude Code
**Version 2.0 "Abete" · Synced with the live site 2026-06-13 · Paste at the start of every development session**
*(v1 "Forest Teal" archived in the boot-website repo at `.superdesign/design-system-v1-teal-reference.md`.)*

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

OffTheBoot uses a fully defined design system. All tokens live in `tokens.css` (this repo) and `app/globals.css` (the live site). **Never hardcode any colour, font, or spacing value — always use CSS variables.**

### Colours — "Abete" palette

| Variable | Hex | Name | Use |
|---|---|---|---|
| `--color-primary` | `#1E2A1A` | Abete | Dark fir green — structural, dark strips, primary buttons, accent-on-light |
| `--color-accent` | `#D6AE5C` | Oro (gold) | Price/duration badge **backgrounds ONLY** |
| `--color-cta` | `#9B3940` | Bordeaux | CTA buttons ONLY — one per section maximum (hover `#7E2E34`) |
| `--color-ink` | `#131C10` | Nero bosco | All text + the darkest section backgrounds, footer |
| `--color-parchment` | `#E8E2D2` | Lino | **Cream text on dark ONLY** — never a surface |
| `--color-bg` | `#FCFCFC` | Off-white | Page background + light sections — never pure `#ffffff` |
| `--color-muted` | `#6B6457` | Muted | Secondary text, meta, placeholders |
| `--color-border` | `#E4E5DF` | Light border | Card borders, dividers |
| `--color-border-strong` | `#D6D7CF` | Strong border | Section dividers, input borders |
| `--color-teal-mist` | `#E6EADB` | Fir mist | Badge bg, step-number circles, image placeholders |
| `--color-teal-pale` | `#DEE4D6` | Light fir | Light section backgrounds, newsletter, blog TL;DR |
| `--color-teal-soft` | `#A8BE97` | Sage | Accents on dark backgrounds (hero italic, dots) |

*(Token names stay `--color-teal-*` in code but hold fir/sage values. The v1 yellow & green tints are RETIRED.)*

**Critical colour rules:**
- `--color-accent` (Oro/Gold) MUST NEVER be used as text on white — badge backgrounds only.
- `--color-cta` (Bordeaux) maximum ONE per section — never stack multiple CTA-coloured elements.
- `--color-parchment` (Lino) is CREAM TEXT ON DARK ONLY — never a background/surface.
- `--color-bg` is `#FCFCFC` — clean off-white, never pure `#ffffff`.
- The ONLY warm-beige surface is the **"Plan my trip"** strip (uses Lino as its background). Beige appears nowhere else.

**Page colour rhythm (current homepage — "slow travel" structure)** — alternate light & dark; two adjacent light sections are tolerated where the design calls for it (e.g. the lightened manifesto → who-we-are pairing), but never two identical dark sections in a row:
1. Hero — dark photo, *Italy* accent in sage
2. Manifesto banner — light fir-mist tint, dark-green italic text
3. Who we are — off-white (founders intro + photo)
4. Our idea of slow travel (values) — dark fir green, cream text, icon points
5. Image band — full-bleed strip of landscape photos
6. Plan my trip — beige (Lino), inline contact form
7. Inspiration — off-white (example-trip cards)
8. Curated experiences — dark fir green, scrolling cards
9. Free-guide strip — light fir
10. Footer — dark (ink)

### Typography

**Three fonts. Never introduce a fourth.** Satisfy is logo-only — never use it for headings, body, or UI.

| Variable | Value | Use |
|---|---|---|
| `--font-display` | `'Newsreader', Georgia, serif` | All headings, card titles, stat numbers — **weight 600** |
| `--font-body` | `'Source Sans 3', system-ui, sans-serif` | Body text, nav, buttons, labels, badges (italic available) |
| `--font-logo` | `'Satisfy', 'Brush Script MT', cursive` | Logo wordmark ONLY (navbar + footer) — applied via `.logo-wordmark` utility (weight 400) |

**Newsreader rules (display):**
- Weight 600 only — declare `font-weight: 600` on display type.
- Visual weight comes from SIZE and TRACKING as well as the 600 weight.
- Negative tracking on large text: `letter-spacing: -0.02em` at 40px+.
- Use italic (`font-style: italic`) for pull quotes, testimonials, H3 accents (always in `--color-primary`).
- NEVER use for body text, buttons, labels, or nav links.

**Source Sans 3 rules (body/UI):**
- Loaded weights: 400, 500, 600, 700 — italic available at 400.
- The 300 cut exists but is **not loaded**; `--fw-light` maps to 400 as the lightest body weight.
- 400 body text, descriptions, nav · 500 card metadata · 600 button labels & emphasis · 700 badges, eyebrows, overlines.
- NEVER use for page headings or section titles.

**Satisfy rules (logo):**
- Logo wordmark ONLY — never for headings, body, or UI.
- Always applied via the `.logo-wordmark` utility class, weight 400.
- Used in the brand wordmark in navbar and footer; nothing else.

**Type scale (bumped one notch, 2026-06):**
```css
--text-hero:   4.25rem    /* 68px — hero display. One use per page */
--text-h1:     2.75rem    /* 44px — major section headings */
--text-h2:     2rem       /* 32px — sub-section, card titles, blog post titles */
--text-h3:     1.375rem   /* 22px — italic, --color-primary */
--text-body:   1.0625rem  /* 17px — Source Sans 3 400 (bumped to 18px on ≥900px screens) */
--text-ui:     0.9375rem  /* 15px — Source Sans 3 400/500 */
--text-label:  0.8125rem  /* 13px — Source Sans 3 600, uppercase */
--text-xs:     0.6875rem  /* 11px — Source Sans 3 700, uppercase, wide tracking */
```

**Eyebrow / overline pattern** — small uppercase label, used before section titles on inner pages (the homepage no longer uses eyebrows):
```css
font-family: var(--font-body);
font-size: var(--text-xs);
font-weight: 700;
letter-spacing: 0.16em;
text-transform: uppercase;
color: var(--color-muted);
```
Add a short horizontal line before the text using `::before` with `width: 20px; height: 1px; background: currentColor`.

### Google Fonts import

In the Next.js site, fonts are loaded via `next/font/google` in `app/layout.tsx` — never link to the Google Fonts CDN from `globals.css`. For static reference pages (this design-system showcase), use:
```html
<link href="https://fonts.googleapis.com/css2?family=Newsreader:ital,wght@0,600;1,600&family=Source+Sans+3:ital,wght@0,400;0,500;0,600;0,700;1,400&family=Satisfy&display=swap" rel="stylesheet">
```

### Buttons

Every button is **squared** — `border-radius: 0`, 2px border, hover inverts fill → outline. Never pills or rounded.
- `.btn-cta` — Bordeaux fill, inverts to Bordeaux outline on hover (CTA only, one per section).
- `.btn-primary` — Abete fill, inverts to Abete outline.
- `.btn-outline` — Ink outline, inverts to Ink fill.
- `.btn-ghost` — underlined text link, weight 700.

### Badge system

Two badge types only:
```html
<!-- Category / style badges -->
<span class="badge-category">Slow travel</span>
<!-- bg: --color-teal-mist (fir mist) · text: --color-primary -->

<!-- Price / duration badges -->
<span class="badge-price">€1.200</span>
<!-- bg: --color-accent (gold) · text: --color-ink -->
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
Forms:      Tally (embedded iframe for /plan-your-trip) + a native contact form on the homepage
Fonts:      next/font/google — Newsreader + Source Sans 3 + Satisfy (logo only)
```

**Tailwind + CSS variables:** Use Tailwind utility classes where possible. For design-system values (colours, fonts), use the CSS variables via Tailwind's arbitrary value syntax: `bg-[var(--color-primary)]`, `text-[var(--color-ink)]`, `font-[var(--font-display)]`. Or extend `tailwind.config.ts` with the token mapping included in `tokens.css`.

**Sanity integration:** All content-driven sections (homepage blocks, itinerary/inspiration cards, experiences, blog posts) pull from Sanity. The homepage is a `homePage` singleton holding every section's copy + photos; components keep hardcoded fallbacks only as a safety net.

---

## Homepage section reference (what actually shipped)

The live homepage renders, in order: **Hero → Manifesto banner → Who we are → Slow travel values → Image band → Plan my trip (contact form) → Inspiration → Curated experiences → Free-guide strip → Footer.** All copy and photos are edited in the Studio (`/studio` → Home page), not in code.

> The original v1 build plan (TaglineStrip, ItinerariesSection, ValuesStrip, NewsletterSection, etc.) is historical and superseded by the section list above and the page colour rhythm.

---

## Writing tone — copy guidelines

When writing placeholder or real copy for the site:

- **Voice:** Warm, direct, personal. Written by a human, not a marketing team.
- **No:** "Discover amazing experiences", "Unforgettable adventures", "Best-in-class service"
- **Yes:** "Away from the crowds", "The Italy most Italians overlook", "Real local knowledge"
- **CTAs:** Always action-first — "Plan your trip", "Plan my slow trip", "See itineraries", "Read the story"
- **Never mention** "sustainability" directly — use "slow", "local", "community", "human", "ethical"
- **Founder order:** Alice before Cesare wherever both are named.
- All copy is in **English only** — even if you see Italian names or places.

---

## WCAG accessibility requirements

All components must meet these minimum contrast ratios:
- Body text on background: minimum 7:1 (AAA)
- UI text on coloured bg: minimum 4.5:1 (AA)
- CTA button (`--color-cta` Bordeaux on white): passes AA
- Cream (Lino) on dark fir, and Bordeaux on white, both pass AA
- Never place `--color-accent` (Gold) as text on white — fails as text; badge backgrounds only

Interactive elements must be identifiable by shape and label, not colour alone.

---

## Quick reference — what to do if unsure

| Question | Answer |
|---|---|
| Which background for a new section? | Off-white (`--color-bg`) or a light fir tint (`--color-teal-pale`) — alternate with dark fir; avoid two identical dark sections in a row |
| Which font for a heading? | Newsreader (`--font-display`), weight 600 |
| Which font for a paragraph? | Source Sans 3 (`--font-body`, weight 400) |
| Which font for the logo? | Satisfy, via `.logo-wordmark` utility — never anywhere else |
| Which colour for a button? | CTA buttons → `--color-cta` (Bordeaux). All other buttons → `--color-primary` or outlined. All buttons are SQUARED (`border-radius: 0`) |
| Can I add a new colour? | No. Use the Abete palette. If something feels missing, ask first |
| Can I use pure white `#fff`? | No. Always `var(--color-bg)` which is `#FCFCFC` |
| Beige anywhere? | Only the "Plan my trip" strip (Lino bg). Nowhere else |
| What tracking for big titles? | `letter-spacing: -0.02em` at 40px+, `-0.01em` at 28px |
| What tracking for uppercase labels? | `letter-spacing: 0.16em` minimum |
