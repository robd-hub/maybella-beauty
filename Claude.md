Maybella Beauty — Site Rebuild
Static mockup of maybellabeauty.com, built to pitch migrating the real business off Shopify ($40/mo) onto free static hosting (GitHub + Vercel). No framework, no build step — plain HTML/CSS/JS on purpose, so it's cheap to host and easy for a non-technical owner's designer (Rob, designimp.com) to maintain without relearning a CMS.
Who this is for
May Balabbo — founder/owner of Maybella Beauty, a Philippine lip tint/gloss brand. She's a friend of Rob's, not a serious e-commerce operator. Her personal email is mbalabbo@gmail.com (for Rob's own reference/reaching her directly — not the public business contact address). The site's public email is maybellashopify@gmail.com (changed Sept 2026 from the original info@maybellabeauty.com — that inbox wasn't actively monitored; maybellashopify@gmail.com is tied to her Shopify account and is checked).
Rob (DesignImp) — building this as a free-mockup pitch (his standard outreach play: build the thing first, then offer it). See project context: he runs designimp.com, flagship reference piece is ayuribeauty.com.
Critical context — read before changing scope
May currently has no live cart/checkout in practice. Her Shopify store has a payment portal configured, but she actually takes orders by DM and gets paid via GCash QR code, manually. This is a deliberate, confirmed decision (not an oversight):

This site is a visual mockup only — no real cart, checkout, or payment processing.
Every "Order Now" / "Shop" CTA routes to the Contact page, which offers email/Facebook/Instagram/TikTok as ordering channels plus a GCash payment explainer.
Don't add a shopping cart, Stripe/PayMongo integration, or inventory system unless a human explicitly asks for that — it would be solving a problem May doesn't have and adds real maintenance burden (payment gateway account, PCI scope, someone has to keep stock counts current).
If a future request does ask for real checkout, treat it as a scope change worth flagging back to the user first, not something to just build — it changes the hosting cost/complexity story that's the whole point of this migration.

contact.html has a "Send a Message" form (Name/Email/Message, added Sept 2026) as an additional way to reach out. It's mailto-based, not a real backend submission — deliberately, to keep the "no framework, no build step, no backend" constraint intact (a real form-processing backend, even a free third-party one, is the same category of complexity-add as cart/checkout and should be flagged back to the user first if ever requested). On submit, JS (script.js) builds a mailto: link to May's personal address (mbalabbo@gmail.com — confirmed by Rob, flagged once for a spelling discrepancy in an earlier message) and opens the visitor's own email client with the message pre-filled; the visitor still has to hit send themselves. This is why it targets her personal inbox rather than the public business address — that one (formerly info@maybellabeauty.com, now maybellashopify@gmail.com) isn't the form's target even though it's actively monitored now, since the form was built before the email swap and nobody's asked to change that yet.
What's real vs. invented
Content was pulled from the live maybellabeauty.com (as of Sept 2026) via fetches of the homepage, /collections/all, /collections/maybella-lip-gloss, /pages/about-us, /pages/contact-us, /pages/faq-s, and /pages/reseller-programme. Treat as real / verified:

All 16 product names, shades, and prices (10 matte lip tints ₱149, 5 lip gloss ₱180, 1 loose powder ₱220)
Founder story, mission, vision, "May Balabbo" name and bio quote (about.html's Our Story/founder copy was expanded Sept 2026 with fuller text Rob provided directly from the brand's real About Us copy — not scraped, pasted verbatim from Rob with only light edits for site tone and to remove the em dash and the old maybellabeauty.com URL reference)
All 9 FAQ questions (answers lightly edited — see below)
Reseller programme copy (4-step process, perks, "no franchise fee", 24–48hr response time)
Contact channels: maybellashopify@gmail.com (public business email, changed Sept 2026 from info@maybellabeauty.com), Facebook business page (facebook.com/profile.php?id=100089975888895 — this is the real Maybella page, used as the primary Facebook link sitewide), Instagram @maybellabeauty (instagram.com/maybellabeauty), TikTok @maybellasignature (tiktok.com/@maybellasignature — confirmed by Rob Sept 2026; note the handle differs from the @maybellabeautyph originally guessed from the live site's copy, since that URL was never confirmed)

May also has a personal/hobby Facebook profile (facebook.com/profile.php?id=61550115153456) with 2.6M+ followers — not a Maybella business channel, so it isn't used as a "contact us" link, but it's real social proof worth surfacing. Acknowledged on about.html as a small "Followed by 2.6M+ on Facebook" line under the founder bio, linking out to that profile.
Nav structure and page names

Real brand assets (added Sept 2026): a real photo of May (assets/hero-may.jpg, cropped from a full-page screenshot of the live homepage) is on the homepage hero banner and cropped into the founder photo circle on index.html and about.html (assets/founder-may.jpg — re-cropped wider in a later pass, the first crop was too tight on her face). Rob went back and forth on recoloring hero-may.jpg's background from its original coral pink (#F0999F) to the site's --rose brand color (#c04f67) — tried it (worked on the wide desktop crop via a color-distance mask, but caused visible blotching on May's skin highlights when the same technique was tested on tighter crops like founder-may.jpg/hero-may-mobile.jpg, since her bright highlights are colorimetrically close to the pink backdrop), reverted, redid it, then reverted again. As of the latest revert, all three images (hero-may.jpg, founder-may.jpg, hero-may-mobile.jpg) are back to the original coral pink background. If this comes up again, the working recolor approach (color-distance mask, background shifted to rose) is proven for the wide desktop hero — just not for tighter crops, which would need manual retouching.

The wide hero-may.jpg (3840x1440) looked bad on mobile — squished into a short strip with May tiny amid empty pink space — so index.html now uses a <picture> element: assets/hero-may-mobile.jpg (a tighter ~1020x970 crop, full wordmark + product + figure, minimal dead space) swaps in via a max-width:600px media source, desktop keeps the original wide banner unchanged. A current logo file (assets/logo.webp, "Maybella Logo.webp" as provided — a plain sans-serif wordmark, distinct from the cursive logo baked into the product photography) is in the header nav on all 8 pages. Real product photography (professional studio shots, provided directly by Rob — not scraped from the live site) is now wired in for every product on the site: all 10 matte lip tints, all 5 lip gloss shades, the Shimmer line (3 shades), Sunscreen Gel, and Fairy Glow Powder (assets/fairy-glow-powder.webp — added last, cropped from a wider promo shot to exclude the oversized logo lockup and match the other products' tight product-only framing). No CSS gradient swatches remain anywhere on the site. Source photos live in assets/lip-tint/, assets/lip-gloss/, assets/shimmer/, assets/sunscreen-gel.webp, and assets/fairy-glow-powder.webp. Note: the files in Dropbox/May/Maybella (old logo files, product trio photos) are separate and stale — do not use them as a source for anything without checking with Rob first.

New product line (added Sept 2026): **Shimmer** — a 3-shade lip tint line (Fairytale, Magical, Mermaid) at ₱120 each, not present on the original live site. Has its own page (shimmer.html) matching the Lip Tint/Lip Gloss pattern, linked from nav and footer on all 8 pages. Also new: **Sunscreen Gel** (SPF 50+, ₱149), added to the "Also from Maybella" section on lip-gloss.html alongside Fairy Glow Powder. Both the Shimmer line and Sunscreen Gel's existence/pricing came directly from Rob this session, not from the original live-site scrape — treat as real but flag to May for confirmation before this goes live, same bar as the rest of "what's real."

Invented / placeholder — flag to Rob before treating as final:

GCash QR box (contact.html, .qr-box): a dashed placeholder that says "Your GCash QR code goes here" — intentionally not a real scannable graphic. Replace with May's actual QR image when she provides one.
FAQ payment answer: original site's FAQ said "Visa, Mastercard, PayPal via checkout" (leftover Shopify boilerplate that doesn't reflect reality). Rewritten here to say GCash + bank transfer via DM, matching how May actually operates. If May starts using a real checkout later, this needs to change back.

Not built at all (present on the real site, out of scope so far): /policies/* pages (refund, privacy, terms, contact-information), Shopee/Lazada/TikTok Shop storefront links (real site lists these as "coming soon" — copy already reflects that).
Structure
Flat static site, no build tooling:

index.html       Home

about.html       About / founder story / mission & vision

lip-tints.html   Matte Lip Tint collection (10 shades)

lip-gloss.html   Lip Gloss collection (5 shades) + Fairy Glow powder + Sunscreen Gel

shimmer.html     Shimmer lip tint collection (3 shades) — new Sept 2026

reseller.html    Reseller Programme

faq.html         FAQ accordion

contact.html     Contact channels + GCash explainer

style.css        All styles — single shared file

script.js        Mobile nav toggle, active-link highlight, FAQ accordion

assets/          Real photos — see "Real brand assets" above for full breakdown; also favicon.ico, favicon.png, apple-touch-icon.png (generated Sept 2026 — a black "M" monogram in Didot on a white rounded square; linked in the <head> of all 8 pages. First version used the brand --rose color, changed to black-on-white per Rob's request.)

Each HTML page duplicates the header nav and footer inline (no templating/includes, since there's no build step). If you add a page or change nav/footer, update it in all 8 HTML files — there's no single source of truth for the header/footer markup. If this becomes a maintenance pain, worth migrating to a static site generator (Astro/11ty) or at least a tiny build script that injects partials — not done yet because the brief was "keep it free and simple."
Design system
Restyled Sept 2026 to match Rob's AYURI-STYLE-GUIDE.md (the design-system reference extracted from ayuribeauty.com, his other project) — same editorial/boutique look and feel, applied within Maybella's existing plain-CSS architecture rather than switching to Tailwind (CLAUDE.md's "no framework" rule wins; the guide's own Tailwind snippets were adapted to hand-written CSS custom properties instead). Defined as CSS custom properties at the top of style.css:

--rose (#e49ea0) / --rose-dark (#d97578) / --rose-light (#f3d0d1) / --rose-pale (#fbf1f1) — primary brand accent (rose = action/interactive: buttons, links, prices). Several rounds Sept 2026: from magenta-pink (#c04f67) → a WCAG-safe coral (#d25042) → Rob supplied a dusty-rose swatch (#e49ea0) → tried a deeper WCAG-safe version of that swatch's hue (#ca4043) → Rob asked for the literal swatch value regardless. Now uses #e49ea0 exactly as supplied. Since that's too light for white text (2.17:1, fails WCAG's 4.5:1), button/pill text was switched from white to var(--ink) everywhere --rose is a solid background (.btn-primary, .nav-cta, .footer-social a:hover, .step .num) — 7.82:1 contrast, reads clearly. --border/--border-alt and --cream-dark stay derived from whatever --rose is, so they moved too.
--gold (#c9a96e) / --gold-soft / --gold-text / --gold-line — secondary/decorative accent (eyebrow labels, the hairline divider under every H1/section H2, founder "role" label)
--cream (#ffffff) / --cream-dark (#fdf0f3) — backgrounds (site is white-based now, not the old cream wash)
--ink (#2d1520) / --ink-soft / --ink-faint — text colors, never pure black
--border (#fad4de) / --border-alt (#fde8ee) — 1px card borders, used instead of box-shadow on all cards/buttons (shadow is reserved for photos only, tinted with the ink color: 0 6px 18px rgba(45,21,32,.12))
Fonts: Cormorant Garamond (headings, serif, font-weight 300 for H1/section H2) + Lato (body, sans, font-weight 300 default), loaded from Google Fonts via <link> in each page's <head>
--radius: 16px for cards; buttons/pills are always border-radius 999px, uppercase, letter-spacing tracked, never shadowed
Signature motif: a centered 1px gold hairline divider (~48px wide) under every page H1 and section-head H2, via a ::after pseudo-element — no markup changes needed per page, it's driven purely by CSS so new headings pick it up automatically as long as they use the existing h1/.section-head h2 markup pattern.

Keep new components consistent with these tokens rather than inventing new colors ad hoc. The Instagram/Facebook/TikTok/Email icons stay inline SVG per the guide's icon rule (no icon font/library).
Hosting / deployment
Currently deployed as a preview deployment to Vercel's scratchpad project (a shared personal scratch project under the designimp-projects team) — this is temporary, not the real home for this site. Live preview: see handoff notes for current URL, or redeploy.
No GitHub repo exists yet. This needs to be pushed to a new repo before setting up Vercel's git integration (auto-deploy on push). Once a repo exists, use Vercel's create_git_project (or the dashboard) to link it — don't keep manually re-uploading files via deploy_to_vercel, that's a stopgap.
Note: Vercel's free Hobby tier is intended for non-commercial projects. Since this will eventually generate revenue for May, plan to move to a paid plan (~$20/mo) once it's live for real — still far cheaper than Shopify's $40/mo, but worth being upfront about with the client.
The Vercel account in use (designimp-projects team) does not have permission to create new projects directly via the API/MCP tool — deployments had to reuse an existing project name. If creating a dedicated maybella-beauty project, it may need to be done from the Vercel dashboard by a team admin first.
Working conventions
No package.json, no npm install, no build command — Vercel auto-detects this as a static site. Keep it that way unless there's a real reason to add a framework.
Test changes by opening the HTML files directly or via a simple local server (python3 -m http.server) before redeploying.
This is a pitch/mockup artifact aimed at a non-technical small business owner and her designer — prioritize clarity and easy hand-editing over cleverness.


