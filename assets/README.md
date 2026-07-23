# Assets — files to drop in

Filenames and folders are already wired into `index.html`. Match the names exactly
and the site picks them up with no code change.

## `assets/img/`

| Filename | Size | Aspect | Used for |
|---|---|---|---|
| `hero-clinic.jpg` | 1920 × 1080 | 16:9 | Hero background |
| `about-team.jpg` | 1000 × 1250 | 4:5 | About section portrait |
| `og-share.jpg` | 1200 × 630 | 1.91:1 | WhatsApp / Facebook / X link previews |

## `assets/img/team/`

Dentist portraits for the Our Dentists section. All four at **800 × 1000 (4:5)**.

| Filename | Dentist |
|---|---|
| `dr-rusman-adlan.jpg` | Dr. Mohd Rusman Adlan B. A. Rahman |
| `dr-noor-syafizah.jpg` | Dr. Noor Syafizah |
| `dr-ahmad-haidhar.jpg` | Dr. Ahmad Haidhar Izzuddin |
| `dr-aiman.jpg` | Dr. Aiman |

Shoot all four the same way — same background, same lighting, same crop from
roughly mid-chest up, eyes on about the same line. The cards sit in a row of four,
so mismatched framing is very obvious. Clinic uniform or scrubs is fine; a plain
light wall works best against the white cards.

If a dentist has not been photographed yet, leave their `onerror` fallback in
place rather than substituting a stock portrait — a stock face presented as clinic
staff is the one thing that will undermine the whole page.

**Art direction.** Warm, human, real. People and interiors — reception, the
treatment room, staff at work. Avoid macro close-ups of teeth and avoid generic
stock: the design leans on these reading as the actual clinic.

**Hero specifics.** A dark `#1A1614` scrim sits over this image at 70% so the
white headline stays legible, which means a bright, evenly lit photo works far
better than a dark one. Keep the left half of the frame relatively uncluttered —
the headline and buttons sit there. Faces and detail read best on the right third.

**Export.** JPG, quality 80, sRGB, stripped of EXIF. Aim under 400 KB for the
hero and under 250 KB for the others. If you have the tooling, also export
`.webp` next to each file; if you do, tell your developer so the `<img>` tags can
be upgraded to `<picture>`.

**After dropping the files in:** delete the `onerror="..."` attribute from both
`<img>` tags in `index.html` (search for `onerror`). It only exists so the page
previews with stand-in photos before the real ones land, and it should not ship.

## Logo files already built

| File | What it is |
|---|---|
| `assets/favicon/favicon.svg` | The disc mark — gold circle, white molar. Live and working. |
| `assets/img/logo-full.svg` | Stacked lockup: KLINIK PERGIGIAN over the mark with ALAN ADLAN inside the tooth. |
| `../logo-3d.html` | 3D model of the mark. Exports `.glb`, `.obj` and `.stl`. |

All three are **hand-traced from the supplied logo images**, not the original
artwork. They match closely at screen sizes. Before any print, signage or
fabrication work, send the original vector file (`.ai`, `.eps` or `.svg`) and
replace the tooth outline in all four places it appears:

- `index.html` — the navbar mark and the footer mark
- `assets/favicon/favicon.svg`
- `assets/img/logo-full.svg`
- `logo-3d.html` — the `TOOTH_PATH` constant

Note that `logo-full.svg` uses live `<text>` for the two wordmarks rather than
outlines, so it depends on Playfair Display being installed. That is fine on the
website but not safe for print — convert both `<text>` elements to outlines
first, or use the original artwork.

## `assets/favicon/`

`favicon.svg` is done. The raster fallbacks below are still needed, for older
browsers and for iOS home-screen icons:

| Filename | Size |
|---|---|
| `favicon.ico` | multi-size: 16, 32, 48 |
| `favicon-32x32.png` | 32 × 32 |
| `favicon-16x16.png` | 16 × 16 |
| `apple-touch-icon.png` | 180 × 180 |

Use the gold circle mark with the tooth cut out. At 16px the wordmark is
unreadable, so use the mark alone. Give `apple-touch-icon.png` an opaque
background — iOS does not respect transparency and will render it black.

`realfavicongenerator.net` produces this whole set from one square source image.

## Not stored here

The `og:image` and `twitter:image` meta tags need an **absolute URL**, because
link scrapers do not resolve relative paths. They currently point at
`https://alanadlandental.com.my/assets/img/og-share.jpg`. When the final domain is
confirmed, update those two tags along with the other domain references flagged
in the TODO comment near the top of `index.html`.
