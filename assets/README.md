# Assets

Everything here is wired into `index.html` by exact filename — match the names and
the site picks files up with no code change.

The clinic's two supplied images are kept untouched in **`assets/img/source/`**:
`logo-original.png` (the gold logo lockup) and `storefront-original.png` (the shop
at dusk). Every derivative below is generated from those two, so they are the
masters — re-crop from them, never from a derivative.

---

## Done — built from the real artwork

| File | Size | Built from | Used for |
|---|---|---|---|
| `img/hero-clinic.jpg` | 1920 × 934 | storefront | Hero background |
| `img/logo-mark.png` | 256 × 256, transparent | logo | Navbar + footer mark |
| `img/og-share.jpg` | 1200 × 630 | logo | Link-preview card |
| `favicon/favicon.ico` | 16/32/48 | logo | Browser tab (legacy) |
| `favicon/favicon-32x32.png` | 32 × 32 | logo | Browser tab |
| `favicon/favicon-16x16.png` | 16 × 16 | logo | Browser tab |
| `favicon/apple-touch-icon.png` | 180 × 180 | logo | iOS home screen |

Notes:

- **`logo-mark.png`** is the gold disc cropped from the logo, with its white
  surround flood-filled to transparency so it sits cleanly on the dark footer. The
  white tooth inside stays opaque (it is enclosed by the gold ring, so the fill
  never reaches it). This is the real artwork, not a trace.
- **`hero-clinic.jpg`** carries a heavy ink scrim in the page. Measured worst-case
  white-text contrast over it is 13.5:1 (AA needs 4.5:1), so legibility is safe
  even though it is a bright sunset shot.
- **`apple-touch-icon.png`** has an opaque white background, as iOS ignores
  transparency and would otherwise render it on black.

---

## Still needed — dentist and team photography

These are the only images still on placeholder fallbacks. Until the real files
land, the `<img>` tags fall back to a stand-in via their `onerror` attribute.

### `img/about-team.jpg` — 1000 × 1250 (4:5)

About-section portrait. A dentist with a patient at the chair, or the team in the
clinic. Warm, real, not stock. If it becomes a photo of Dr. Mohd Rusman Adlan
specifically, update the `alt` text on that `<img>` to name him.

### `img/team/` — four dentist portraits, 800 × 1000 (4:5)

| Filename | Dentist |
|---|---|
| `dr-rusman-adlan.jpg` | Dr. Mohd Rusman Adlan B. A. Rahman |
| `dr-noor-syafizah.jpg` | Dr. Noor Syafizah |
| `dr-ahmad-haidhar.jpg` | Dr. Ahmad Haidhar Izzuddin |
| `dr-aiman.jpg` | Dr. Aiman |

Shoot all four the same way — same background, lighting and crop (mid-chest up,
eyes on the same line). They sit in a row of four, so mismatched framing shows
badly. A plain light wall works best against the white cards. If a dentist has not
been photographed, leave their `onerror` fallback rather than substituting a stock
face — a stock portrait presented as clinic staff undermines the whole page.

**Export for all photos.** JPG, quality ~82, sRGB, EXIF stripped. Under 400 KB for
the hero, under 250 KB each for portraits. If you can also export `.webp`, tell
your developer so the `<img>` tags can be upgraded to `<picture>`.

**After dropping any photo in:** delete that image's `onerror="…"` attribute in
`index.html` (search `onerror`). It only exists so the page previews before the
real files land, and it should not ship.

---

## Other logo files

| File | What it is |
|---|---|
| `img/logo-full.svg` | Stacked lockup: KLINIK PERGIGIAN over the mark, ALAN ADLAN inside the tooth. |
| `favicon/favicon.svg` | Hand-traced flat-gold version of the mark. No longer linked from `index.html` (the real-art `.ico`/PNG favicons replaced it); still used as the favicon for `logo-3d.html`. |
| `../logo-3d.html` | 3D model of the mark. Exports `.glb`, `.obj`, `.stl`. |

`logo-full.svg` and `logo-3d.html` are still **hand-traced** from the supplied
images — fine on screen, but for print, signage or fabrication send the original
vector (`.ai`, `.eps`, `.svg`) and replace the outline. `logo-3d.html` holds it in
the `TOOTH_PATH` constant; `logo-full.svg` uses live `<text>` for the wordmarks
(depends on Playfair Display — convert to outlines before print).

The navbar and footer marks in `index.html` now use the real `logo-mark.png`, so
they need no trace replacement.

---

## Domain note

`og:image` and `twitter:image` need an **absolute URL** — scrapers ignore relative
paths. They point at `https://alanadlandental.com.my/assets/img/og-share.jpg`.
When the final domain is confirmed, update those two tags along with the other
domain references flagged in the TODO near the top of `index.html`.
