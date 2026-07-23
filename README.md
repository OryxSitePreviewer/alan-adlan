# Klinik Pergigian Alan Adlan — website

Marketing site for Klinik Pergigian Alan Adlan, a dental clinic in Seksyen 1,
Bandar Baru Bangi, Selangor.

Single static page. No build step, no package manager, no framework.
Open `index.html` in a browser and it runs.

## Files

| Path | What it is |
|---|---|
| `index.html` | The entire website. Everything is in this one file. |
| `logo-3d.html` | 3D model of the logo mark. Exports `.glb`, `.obj`, `.stl`. |
| `assets/` | Images, favicons, logo files. See `assets/README.md`. |
| `PLAN.md` | Design decisions — colour tokens, typography, layout, assumptions. |

## Stack

- Tailwind CSS via CDN, pinned to `3.4.16`, palette configured inline
- Google Fonts: Plus Jakarta Sans (headings), Inter (body), Playfair Display (wordmark only)
- Vanilla JS for the mobile menu and navbar scroll state — nothing else
- `logo-3d.html` additionally loads Three.js `0.170.0` from a CDN

## Local preview

No server needed:

```bash
start index.html
```

If you prefer to serve it over HTTP (closer to production, and required if you
later add anything that fetches files):

```bash
python -m http.server 8000
```

## Accessibility and layout, as verified

- No horizontal scroll at 320, 375, 768, 1024 and 1440px
- All body text meets WCAG AA contrast; gold `#C9A227` is used as a fill only,
  never as text on white, because it measures 2.4:1 there
- Visible keyboard focus rings on every interactive element
- `prefers-reduced-motion` honoured for smooth scroll, transitions, animations
  and the 3D auto-rotate
- One `h1`, logical heading order, semantic landmarks

## Before launch

Full list in the TODO comments in `index.html`. The blocking ones:

1. **Dentist sign-off.** The four profiles in the Our Dentists section were
   assembled from public sources, not written by the dentists. Each must approve
   their own card. Missing: qualifications for Dr. Mohd Rusman Adlan and
   Dr. Ahmad Haidhar Izzuddin, and Dr. Aiman's full legal name.
2. **Photos and raster favicons.** Filenames and sizes are specified in
   `assets/README.md`. After dropping them in, delete the six `onerror`
   attributes in `index.html` — they exist only so the page previews with
   stand-in images.
3. **Final domain.** `alanadlandental.com.my` is a placeholder. It appears in the
   canonical tag, `og:url`, `og:image`, `twitter:image`, and the JSON-LD `@id`
   and `url`.
4. **Original logo vector.** Every logo file here is hand-traced from supplied
   images. Fine on screen, not fine for print or fabrication. Replacing it means
   updating the outline in four places — listed in `assets/README.md`.
5. **Phone number discrepancy.** Clinic artwork shows `03 8926 1697`; the brief
   gave `019-4231697`. Only the brief's numbers are published. Confirm which is
   current.

## Content rules applied

Nothing on this site was invented. No prices, no years in business, no awards, no
patient outcomes, and no credentials beyond what the clinic supplied. Testimonials
are verbatim Google reviews. Dentist interests are worded as "special interest in",
never "specialist in" — under Malaysian Dental Council advertising rules that term
is reserved for dentists on the National Specialist Register.
