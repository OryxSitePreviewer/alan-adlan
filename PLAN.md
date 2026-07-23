# Build Plan — Klinik Pergigian Alan Adlan

Single-file marketing site (`index.html`), Tailwind CDN (pinned), no build step.

> **Revision 2** — palette changed from cool teal to the clinic's actual gold
> branding, per client feedback. Typography, rhythm and placeholder decisions
> from revision 1 are unchanged and approved.

---

## 1. Colour tokens

Elegant, warm, restrained. Gold does the branding work; near-black does the
reading work; white is the canvas. One accent family, no competing hues.

| Token | Hex | Role |
|---|---|---|
| `ink` | `#1A1614` | Warm near-black. Headings, footer background, **and text on gold**. |
| `stone` | `#6B625B` | Body copy, secondary text, captions. 5.9:1 on white. |
| `gold` | `#C9A227` | The brand gold. Logo circle, button fills, icon fills, rules, highlights. |
| `gold-deep` | `#8A6A12` | Hover/active, focus ring, and any gold-coloured **text**. 5.1:1 on white. |
| `porcelain` | `#FAF7F2` | Off-white alternating section background. Barely-there warmth. |
| `line` | `#ECE6DC` | Hairlines, card edges, dividers. Never a heavy border. |

White (`#FFFFFF`) is the base canvas; `porcelain` alternates.

### The contrast rule this palette has to respect

Gold at `#C9A227` is only **2.4:1** on white — it can never carry body text.
So the design splits gold into two jobs:

- **`gold` is a fill, never a text colour.** Buttons are gold with `ink` text
  (**7.5:1**) — which is also the more elegant treatment. Icons, the logo circle,
  the star row, and decorative rules use gold as a fill, all as non-text elements
  above the 3:1 UI threshold or paired with a text label.
- **`gold-deep` is the text/stroke gold.** Inline links, small labels, and the
  focus ring use `#8A6A12` — 5.1:1 on white, 5.0:1 on porcelain, and 3.5:1 on the
  `ink` footer, so one focus-ring colour works on every background.

All body text is `stone` or `ink`. All button text is `ink` on gold or white on
`ink`. Nothing under 4.5:1 carries a sentence.

### WhatsApp CTA

Gold with `ink` text, same as every other primary action — not WhatsApp green.
Palette stays unified.

## 2. Typography

Google Fonts, two families, sans throughout — elegant clinic, not tech startup.

- **Display — Plus Jakarta Sans** (300/400/600). Headings at *light* weight
  (300) and generous size (h1 clamps 2.25rem → 3.75rem), with slightly negative
  tracking. Light-weight-at-large-size is what keeps it reading as refined rather
  than punchy.
- **Body — Inter** (400/500). 17px desktop / 16px mobile, relaxed leading,
  comfortable measure (~65ch).

The "elegant" cues, concretely: no heavy weights above 600 anywhere, no all-caps
except small tracked eyebrow labels, thin gold hairlines instead of chunky
dividers, 1.5px icon strokes, and generous letter-spacing on the logo lockup.

Loaded with `preconnect` + one stylesheet call, `display=swap`.

## 3. Section order & layout approach

Container: `max-w-[1200px]`, `px-5 sm:px-6 lg:px-8`.
Section padding: `py-14 md:py-20 lg:py-28` (≈56px mobile → 112px desktop).

| # | Section | id | Layout |
|---|---|---|---|
| 1 | Sticky navbar | — | Flex row: gold-circle logo mark + wordmark left, links right, gold Book Appointment button far right. White throughout; **scroll state** adds a shadow and firms the bottom hairline past 12px. Hamburger + drop panel under 768px (`md`). |
| 2 | Hero | `#home` | Full-bleed image, `ink` scrim + left-to-right gradient so white text clears 5:1 across the whole text zone. Content in `max-w-2xl`. WhatsApp CTA primary (gold/ink), Call Us secondary (white outline). |
| 3 | Trust strip | — | Immediately under hero on `porcelain`. 3-up grid: hours, location, 4.8 rating. Gold icons, `stone` labels, thin gold rules between at `md`. |
| 4 | About | `#about` | Two-column 5/7 at `lg`, stacked below: 4:5 portrait image left, copy right. Community and practice only — no invented credentials. |
| 5 | Services | `#services` | 3-col at `lg`, 2 at `sm`, 1 at base. `rounded-2xl` white cards on `porcelain`, `line` hairline, shadow lifts on hover. Inline SVG icon per card in a gold-tinted circle. |
| 6 | Reviews | `#reviews` | Centred stat block leading with 4.8 ★ / 330+, gold star row, then 3 testimonial cards. |
| 7 | Contact & Location | `#contact` | Two-column 5/7 at `lg`: details (address, hours, both tap-to-call numbers, WhatsApp button, socials) + map iframe in a rounded overflow-hidden frame, 4:3. |
| 8 | Footer | — | `ink` background, gold hairline top, 3 columns (brand, quick links, contact + social), copyright bar. |

**Logo:** inline SVG — a gold filled circle with a white tooth cut out of it,
beside a two-line wordmark. Scales cleanly, no image request, works in the footer
inverted.

**Photo treatment:** wide, warm, human — patients, staff at work, clinic
interiors. Not macro teeth. `rounded-2xl`, no filter, no duotone. Placeholders at
the correct aspect ratio, each preceded by an HTML comment naming the real shot.

## 4. Technical approach

- Tailwind Play CDN pinned to `3.4.16`; palette in an inline `tailwind.config`
  before the runtime pass.
- Small `<style>` block for: font stacks, `:focus-visible` ring (2px `gold-deep`,
  2px offset — one colour, passes 3:1 on white, porcelain and ink),
  `scroll-behavior: smooth` + `scroll-margin-top` so the sticky header never
  covers a heading, and a `prefers-reduced-motion: reduce` block killing smooth
  scroll, transitions and animations.
- Vanilla JS, ~40 lines: mobile menu toggle with `aria-expanded`,
  close-on-link-click, Escape to close, and a scroll listener for the header
  state. Smooth scroll is CSS, so reduced-motion is honoured without JS branching.
- `overflow-x: hidden` on `body`, no fixed-width children, long strings allowed to
  wrap — verified at 320 / 375 / 768 / 1024 / 1440.

## 5. SEO & metadata

- `<title>`: *Dentist in Bandar Baru Bangi | Klinik Pergigian Alan Adlan*
- Meta description targeting "dentist Bandar Baru Bangi", under 160 chars.
- Open Graph + `summary_large_image` Twitter card.
- JSON-LD `@type: Dentist` — `address`, `geo`, `openingHoursSpecification`
  (Mo–Su 09:00–21:00), both `telephone` numbers, `aggregateRating` 4.8 / 330,
  `sameAs` for Instagram + TikTok.
- Exactly one `<h1>` (hero). Sections `h2`, cards `h3`.
- `lang="en"` with a comment noting where a Malay version would hook in.

## 6. Assumptions

1. **Geo coordinates** — approximate Seksyen 1, Bandar Baru Bangi
   (2.9698, 101.7690), marked TODO for the exact Google Maps pin. *(Approved.)*
2. **Map embed** — keyless `maps.google.com/maps?q=...&output=embed` for the
   address, with a comment marking where the official *Share → Embed a map* code
   goes. *(Approved.)*
3. **Photos** — all placeholder, each with a comment describing the real shot. No
   stock person is presented as clinic staff.
4. **Testimonials** — realistic placeholder copy in a clearly marked comment
   block, initials-only attribution. *(Approved.)*
5. **Facebook** — `href="#"` with a visible TODO comment.
6. **No invented facts** — no dentist names, no years established, no prices, no
   credentials, no treatment outcomes.
7. **Rating disclosure** — 4.8 / 330+ attributed to Google Reviews; no award or
   certification claimed.
8. **Locale** — English with Malaysian-natural phrasing, 12-hour times, no prices.

---

**Status:** approved to build.
