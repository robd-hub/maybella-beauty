# Maybella Beauty — Site Rebuild

A static mockup of [maybellabeauty.com](https://maybellabeauty.com), built to pitch migrating the real business off Shopify ($40/mo) onto free static hosting (GitHub + Vercel). Plain HTML/CSS/JS — no framework, no build step, no backend.

This is a **visual mockup, not a working store**. There's no cart or payment processing — every "Order Now" CTA routes to the Contact page, which explains how May actually takes orders today: DM her, pay via GCash. See [CLAUDE.md](Claude.md) for the full rationale and a detailed real-vs-placeholder breakdown of the content.

## Quick start

No install, no build. Just open the files or serve them locally:

```bash
python3 -m http.server
```

Then visit `http://localhost:8000`.

## Structure

```
index.html       Home
about.html       About / founder story / mission & vision
lip-tints.html   Matte Lip Tint collection (10 shades)
lip-gloss.html   Lip Gloss collection (5 shades) + Fairy Glow powder + Sunscreen Gel
shimmer.html     Shimmer lip tint collection (3 shades)
reseller.html    Reseller Programme
faq.html         FAQ accordion
contact.html     Contact channels + GCash explainer
style.css        All styles — single shared file
script.js        Mobile nav toggle, active-link highlight, FAQ accordion
assets/          Real photos and logo — see below
```

Each HTML page duplicates the header/footer inline — there's no templating. **If you add a page or change nav/footer, update it in all 8 HTML files.**

## Design system

Restyled to match [AYURI-STYLE-GUIDE.md](AYURI-STYLE-GUIDE.md) (Rob's design-system reference from his other project, ayuribeauty.com): Cormorant Garamond + Lato fonts, a blush-pink/gold palette, pill-shaped uppercase buttons, thin-border cards instead of shadows, and a signature gold hairline divider under every heading. Applied via the existing `style.css` custom properties — not a Tailwind rewrite, to keep the "no framework" setup CLAUDE.md calls for.

## Real brand assets

- `assets/logo.webp` — the real Maybella wordmark, used in the header on every page.
- `assets/hero-may.jpg` / `assets/founder-may.jpg` — a real photo of May, cropped from a screenshot of the live homepage, used on the homepage hero banner and the founder photo circle (homepage + About page).
- `assets/lip-tint/*.webp` (all 10 shades), `assets/lip-gloss/*.webp` (4 of 5 shades), `assets/shimmer/*.webp` (all 3 shades), `assets/sunscreen-gel.webp` — real studio product photography.
- **Shimmer** is a new product line (Fairytale, Magical, Mermaid — ₱120 each) not on the original live site, added this session with its own page. **Sunscreen Gel** (₱149) is also new. Both should be confirmed with May before treating as final launch copy.

## Known placeholders

These still need real assets/content before this could go live — see [CLAUDE.md](Claude.md) for the complete list:

- Sexy (Lip Gloss) and Fairy Glow Powder still use CSS gradient swatches — no photo provided for these two yet.
- The GCash QR box (`contact.html`) is a dashed placeholder.
- The TikTok link (`href="#"`) needs May's actual TikTok URL.
- Footer credit ("Design mockup by DesignImp") should be removed if this becomes May's real live site.

## Deployment

Currently a preview deployment on Vercel's shared `scratchpad` project (not git-connected yet). See [Handoff Notes](Handoff%20Notes) for the current preview URL and next steps — no GitHub repo exists yet, which is the first thing needed before setting up auto-deploy on push.

## More context

- [CLAUDE.md](Claude.md) — full project brief: scope decisions, design system tokens, what's real vs. invented, working conventions.
- [Handoff Notes](Handoff%20Notes) — session history, decisions made, open issues, and suggested next steps.
