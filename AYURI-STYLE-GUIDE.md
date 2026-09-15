# AyuriNails Beauty Lounge — Design System Reference

A style guide extracted from the live AyuriNails Beauty Lounge site (ayuribeauty.com), for reuse on other projects. Hand this file to Claude Code in another repo and ask it to apply the same look and feel.

**Stack**: static HTML + Tailwind CSS via CDN (no build step), Google Fonts, vanilla JS. No component framework.

```html
<script src="https://cdn.tailwindcss.com"></script>
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,500;0,600;1,300;1,400&family=Lato:wght@300;400;700&display=swap" rel="stylesheet" />
```

---

## 1. Brand feel

Boutique beauty salon: soft, feminine, editorial, a little luxe. Generous whitespace, thin/light type weights, muted blush-pink and warm gold accents rather than saturated color, rounded-but-not-bubbly corners, low-contrast borders instead of heavy shadows. Nothing shouts — pricing, CTAs and headings stay quiet and let the layout do the work.

---

## 2. Typography

Two families, both Google Fonts:

- **Display / headings**: `'Cormorant Garamond', serif` — a light, elegant serif. Used only for `h1`/`h2`/`h3` and anything with class `.font-display`.
- **Body**: `'Lato', sans-serif` — the default on `body`.

```css
body { font-family: 'Lato', sans-serif; }
h1, h2, h3, .font-display { font-family: 'Cormorant Garamond', serif; }

/* Deliberate weight overrides — Tailwind's own font-light (300) reads
   too thin for body copy at this size, so it's bumped to 400, while
   headings keep the true light 300 weight for that editorial serif look. */
.font-light { font-weight: 400 !important; }
.font-display.font-light { font-weight: 300 !important; }
```

Tailwind config aliases (optional, only needed if you want `font-display`/`font-body` utility classes instead of the CSS above):
```js
fontFamily: {
  display: ['"Cormorant Garamond"', 'serif'],
  body: ['Lato', 'sans-serif'],
}
```

### Scale & usage

| Role | Classes | Notes |
|---|---|---|
| Page H1 | `font-display font-light text-5xl` + `style="letter-spacing: 0.04em;"` | Centered, dark ink color |
| Section H2 | `font-display font-light text-2xl` or `text-3xl` | |
| Card/name H2 | `font-display font-light text-2xl` | e.g. team member names |
| Body copy | `text-sm font-light leading-relaxed text-gray-500` | Muted, generous line-height |
| Eyebrow/label | `text-xs tracking-widest uppercase` in gold `#c9a96e`, or `text-xs tracking-[0.3em] uppercase` | Small caps-style label above/below a heading |
| Nav / button labels | `text-xs tracking-widest uppercase font-light` | Always uppercase + wide letter-spacing |

Headings and eyebrow labels lean on **letter-spacing** (`tracking-widest`, `tracking-[0.25em]`, `tracking-[0.3em]`) far more than font weight or size to create hierarchy — this is a core signature of the look.

---

## 3. Color palette

Primary palette lives as a Tailwind theme extension (`blush` scale), plus a couple of named one-offs:

```js
tailwind.config = {
  theme: {
    extend: {
      colors: {
        blush: {
          50:  '#fef9fa',
          100: '#fdf0f3',
          200: '#fad4de',
          300: '#f4b3c2',
          400: '#e8879a',
          500: '#d4637a',
          600: '#c04f67',
          700: '#9e3d52',
        },
        rose: { dark: '#2d1520' },
        gold: '#c9a96e',
      }
    }
  }
}
```

| Token | Hex | Usage |
|---|---|---|
| `blush-600` / rose | `#c04f67` | **Primary accent.** Buttons, links, active nav state, price highlight, icons |
| `blush-700` | `#9e3d52` | Outlined-pill text/border (jump-nav pills), darker accent |
| `blush-500` | `#d4637a` | Rare — mid-tone accent |
| `blush-400` | `#e8879a` | Rare — mid-tone accent |
| `blush-300` | `#f4b3c2` | Pill/badge borders, jump-nav pill border |
| `blush-200` | `#fad4de` | Card/footer border color, hairline dividers |
| `blush-100` | `#fdf0f3` | Best-Seller badge background, pill hover background, divider stripes (`divide-blush-100`) |
| `blush-50` | `#fef9fa` | Rare, very light wash |
| `rose-dark` | `#2d1520` | Near-black ink for logo wordmark & headings (not pure black) |
| `gold` | `#c9a96e` | Secondary accent — eyebrow labels, divider rule under H1, "Beauty Lounge" subtitle |
| gold-soft | `#fdf4e7` | Signature-badge background |
| gold text | `#a07c3a` | Signature-badge text |
| gold-line | `#e8d5a3` | Signature-badge border |
| card border alt | `#fde8ee` | Slightly different pink used for price-table card borders / mobile-menu divider |
| body text | Tailwind `gray-800` / `gray-600` / `gray-500` / `gray-400` | Ink hierarchy from headings down to captions — deliberately **never pure black** |

**Rule of thumb**: rose (`#c04f67`) = action/interactive/primary; gold (`#c9a96e`) = decorative/editorial accent (dividers, eyebrow text, "Signature" badge); everything else is grayscale + one of the two blush-pink border tones (`#fad4de` or `#fde8ee`).

---

## 4. Layout conventions

- **Container**: `max-width` scoped per page — `max-w-xl`/`max-w-2xl`/`max-w-3xl`/`max-w-4xl mx-auto`, never full-bleed text.
- **Page vertical rhythm**: `<main class="pt-32 pb-24 px-6 ...">` — large top padding clears the fixed nav (nav is ~70–80px tall but pt-32 gives breathing room), generous bottom padding before footer.
- **Hero block pattern** (used at the top of every inner page):
  ```html
  <div class="text-center mb-8">
    <h1 class="font-display font-light text-5xl text-gray-800 mb-2" style="letter-spacing: 0.04em;">Page Title</h1>
    <div class="w-12 h-px mx-auto mb-6" style="background-color: #c9a96e;"></div>
    <p class="text-gray-500 text-sm font-light leading-relaxed max-w-xl mx-auto">
      One short descriptive sentence.
    </p>
  </div>
  ```
  The **gold hairline divider** (`w-12 h-px`, gold background) under every H1 is a signature motif — always centered, always thin, always short.
- **Section spacing**: sections stack with `space-y-16` (major) or `space-y-12`; internal card lists use `divide-y` instead of margins between rows.
- **Grids**: `grid grid-cols-2 sm:grid-cols-3 gap-3` for photo galleries; `grid grid-cols-1 sm:grid-cols-2 gap-6` for card layouts (e.g. team).
- **Breakpoints**: standard Tailwind `sm:`/`md:` plus one custom arbitrary breakpoint `min-[1360px]:` used specifically for the desktop nav vs. mobile hamburger switch (the nav has a lot of links, so it needs more room than Tailwind's default `lg`).

---

## 5. Components

### 5.1 Buttons (always pill-shaped, `rounded-full`)

**Filled primary** (main CTA — "Book Now"):
```html
<a href="#" class="inline-flex items-center gap-2 text-white text-sm font-light tracking-widest uppercase px-7 py-3 rounded-full transition hover:opacity-90" style="background-color: #c04f67;">
  Book Now
</a>
```

**Outlined secondary** (paired next to a filled button, e.g. under a filled "Get Directions"):
```html
<a href="#" class="inline-flex items-center gap-2 text-sm font-light tracking-widest uppercase px-7 py-3 rounded-full border transition hover:bg-white" style="border-color: #c04f67; color:#c04f67;">
  Book Now
</a>
```

**Small inline "Book Now" chip** (used inside a price-list row, next to a service name):
```html
<a href="#" target="_blank" rel="noopener" class="hover:opacity-90 transition" style="display:inline-block;font-size:0.54rem;letter-spacing:0.12em;text-transform:uppercase;background:#c04f67;color:#fff;padding:2px 8px;border-radius:999px;font-weight:400;vertical-align:middle;">Book Now</a>
```

Common traits: `rounded-full`, uppercase + `tracking-widest`, `font-light`, hover = `opacity-90` (filled) or `bg-white` (outlined). No box-shadow on buttons, ever.

### 5.2 Badges / pills

Base pill style (shared shape, swap background/color per variant):
```css
display:inline-block;
font-size:0.54rem;
letter-spacing:0.12em;
text-transform:uppercase;
padding:2px 7px;
border-radius:999px;
font-weight:400;
vertical-align:middle;
```

| Variant | Background | Text | Border |
|---|---|---|---|
| **Signature** (premium/flagship service) | `#fdf4e7` | `#a07c3a` | `1px solid #e8d5a3` |
| **Best Seller** | `#fdf0f3` | `#c04f67` | `1px solid #f4b3c2` |
| **Book Now** (link variant) | `#c04f67` | `#fff` | none, `padding:2px 8px` |

Only ever **one** badge per item — pills are used sparingly to flag a single standout attribute, not stacked.

### 5.3 Cards

```html
<div class="bg-white rounded-2xl p-6 ..." style="border: 1px solid #fad4de;">
  ...
</div>
```
or for list-style cards (price tables):
```html
<div class="bg-white rounded-2xl shadow-sm overflow-hidden divide-y divide-blush-100" style="border:1px solid #fde8ee;">
  <div class="flex justify-between items-center px-6 py-3.5 text-sm">
    <span class="text-gray-600 font-light">Service Name<br/><span class="text-xs text-gray-400 italic">short description</span></span>
    <span class="text-gray-800">₱999</span>
  </div>
  <!-- more rows, divided by divide-y -->
</div>
```
Cards: `rounded-2xl`, a 1px pink-toned border (never a shadow-heavy "floating" card), white background, generous internal padding.

### 5.4 Jump-nav pills (secondary in-page nav)

```css
.jump-pill { border: 1px solid #f4b3c2; color: #9e3d52; padding: 6px 16px; border-radius: 999px; font-size: 0.8rem; }
.jump-pill:hover { background: #fdf0f3; }
```
Laid out as `flex flex-wrap justify-center gap-2`.

### 5.5 Header nav

- `fixed top-0`, full width, `bg-white shadow-sm`, `px-8 py-4`.
- Left: logo image (~54px tall) + two-line wordmark (`AyuriNails` uppercase tracked serif in `#2d1520`, `Beauty Lounge` smaller uppercase gold subtitle underneath).
- Center/right (desktop only, `min-[1360px]:flex`): uppercase tracked-widest nav links (`text-xs`, `text-gray-500`), active page gets inline `color: #c04f67`.
- Filled rose "Book Now" pill at the end of the nav.
- Below `1360px`: hamburger icon button toggles a full-width dropdown panel (`absolute top-full`, white, `border-t`, each link full-width with a bottom hairline `border-color: #fde8ee`), closes on outside-click, Escape key, or link click.

### 5.6 Footer

Centered, single column:
```html
<footer class="py-10 text-center bg-white border-t" style="border-color: #fad4de;">
  <p class="font-display font-light text-xl tracking-[0.25em] uppercase" style="color: #2d1520;">Brand Name</p>
  <p class="text-xs tracking-[0.3em] uppercase mt-1" style="color: #c9a96e;">Tagline</p>
  <p class="text-xs mt-2 font-light text-gray-400">Location line</p>
  <div class="flex flex-wrap justify-center gap-x-5 mt-5 text-xs font-light tracking-wide text-gray-400">
    <!-- footer links, active page in #c04f67 -->
  </div>
  <p class="text-xs mt-4 font-light text-gray-300">© Year Brand. All rights reserved.</p>
</footer>
```
On mobile, the link row switches to a 2-column grid (`grid grid-cols-2 gap-x-4 gap-y-2 text-left px-10`) instead of centered flex-wrap, to avoid ragged line lengths at narrow widths — reverts to the centered flex row at `sm:` and above.

### 5.7 Imagery

- Photos: `rounded-2xl` (cards/galleries) or `rounded-full` (circular headshots), always `object-cover`.
- Gallery grid images get a soft shadow: `box-shadow: 0 6px 18px rgba(45,21,32,0.12);` (shadow tinted with the ink color, not pure black).
- `loading="lazy"` on all below-the-fold images.

### 5.8 Icons

Inline SVG only (no icon font/library), `fill="none" stroke="currentColor" stroke-width="1.5"` (nav/menu icons) or `stroke-width="2"` (smaller UI icons like FAQ chevrons), rounded line caps/joins (`stroke-linecap="round" stroke-linejoin="round"`).

### 5.9 FAQ accordion

```css
.faq-icon { transition: transform 0.2s; }
```
Chevron SVG rotates 180° on open via a `toggleFaq(btn)` JS helper that toggles a `.hidden` class on the answer `<div>` and rotates the icon — no external JS library.

---

## 6. Motion

Minimal. `transition` + `hover:opacity-90` on filled buttons, `hover:bg-white` on outlined buttons, `duration-200` transform on the FAQ chevron. No page-load animations, no scroll-triggered effects.

---

## 7. Voice (for copy, not visuals)

Short, warm, confident sentence fragments rather than full marketing paragraphs. Section intros are one sentence. Service descriptions are one clause ("Best for: ..."). Uppercase tracked-out labels do a lot of the "design" work that bold/color would otherwise do elsewhere.

---

## 8. Quick-start checklist for a new project

1. Load Cormorant Garamond (serif, headings) + Lato (sans, body) from Google Fonts.
2. Add the `blush` color scale + `rose.dark` + `gold` to your Tailwind theme (or use the raw hex values directly).
3. Every H1 gets a centered gold hairline divider underneath (`w-12 h-px`, `#c9a96e`).
4. Buttons are always `rounded-full`, uppercase, `tracking-widest`, `font-light` — filled rose for primary, outlined rose for secondary.
5. Cards are `rounded-2xl` with a 1px pink border (`#fad4de` or `#fde8ee`) — no drop shadows except a very soft one on photos.
6. One badge per item max, from the Signature (gold) / Best Seller (rose) palette above.
7. Keep body copy in gray-500/gray-400, never pure black; keep the ink/heading color at `#2d1520`, never pure black either.
