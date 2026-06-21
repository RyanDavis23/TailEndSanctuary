# Tail End Sanctuary — Professional Build Plan
*Higgsfield asset pipeline + design system + execution sequence. Generated from an 8-agent research run, fact-checked against the live Higgsfield MCP tool schemas (June 21, 2026).*

## The honest thesis
Higgsfield is **not** a "make it professional" button — and for a real 501(c)(3) courting donors, treating it like one would backfire. The split:
- **~80% of "insanely professional" is hand-written front-end craft** — a real `<picture>` art-direction system, type/color discipline, sticky donate, favicon + social cards, the embedded signup form, the Contact-page deletion, consistent green CTAs, accessible video.
- **~20% is Higgsfield *enhancing the founders' REAL photos*** — clean up the logo, upscale low-res phone shots, occasionally re-frame. **We never fabricate a dog.** Every animal on the site stays a real Tail End dog — only cleaned and reframed.

## What Higgsfield actually does here (verified against real tool schemas)
| Use | Real tool | Notes |
|---|---|---|
| Clean the logo (kill screenshot halo → transparent alpha) | `remove_background` | image or video |
| Sharpen low-res photos | `upscale_image` | **fixed `2k`/`4k` enum only** — needs source w/h; exact px is a *local* resize after |
| Sharpen the Teddy video | `upscale_video` | use **topaz** (no source dims needed) |
| Change aspect ratio by regenerating bg (instead of cropping) | `outpaint_image` / `reframe` | **conditional, last resort** — see guardrails |
| Get local files into Higgsfield | `media_upload_widget` | the only way — remote MCP can't read chat/Gmail attachments |

**NOT Higgsfield (local steps, tools already installed):**
- `.mov` → web `.mp4` transcode + poster-frame extraction → **ffmpeg** (`/Users/primary/local/bin/ffmpeg`)
- Exact pixel dimensions, favicon sizes (32/180/512), 4:5 / 21:9 master crops → **sips** (macOS)
- **Never** `motion_control` / image-to-video on a real dog. **Never** `generate_image` of an animal.

## Actual source resolutions (measured via sips)
These are **smaller than the old repo images**, so upscaling genuinely matters; the two reds are mandatory:
| Asset | Source | Action |
|---|---|---|
| logo-new.png | 1254² | remove_bg → upscale 4k → local favicon/@2x sizes |
| home-hero | 1280×890 | upscale 4k → crop 21:9 + 4:5 |
| about-cindy | 960×1280 (portrait) | upscale 4k → 4:5 mobile is native; desktop = wide crop or *small* outpaint |
| dog-teddy/nita/valentino/coffee | ~1100–1400 | upscale 2k → local 4:5 1080×1350 cards |
| **getinvolved-senta** | **640×502** 🔴 | **upscale 4k first**, then crop |
| **donate-hero** | **758×775** 🔴 | **upscale 4k**, **crop only — never outpaint the money page** |
| teddy-video | 15 MB .mov | upscale_video(topaz) → ffmpeg mp4+poster |

## The responsive hero fix (Juanita's #1 cross-page complaint)
The bug is structural: one `<img object-fit:cover>` band forced through both iPhone and iPad, patched with per-page `object-position` guesses. The durable fix is a **`<picture>` art-direction system** per hero:
- **Mobile** source: 4:5 / near-square crop zoomed on the dog (this is the "iPhone shows more depth" Juanita likes) via `<source media="(max-width:600px)">`
- **Desktop** source: wide 21:9 crop for iPad/desktop
- CSS `object-position` per asset as a fallback layer + fixed `aspect-ratio` per breakpoint.
This survives future photo swaps **without re-running any model** — the real engineering ask behind "formats well on one device, not the other."

## Design system
- **Type:** Cormorant (headlines, tracked) / Inter (body); dog quotes in Cormorant italic; body measure ~66ch. Logo's elegant script sets the tone.
- **Color:** warm green = brand + the single unified CTA color (edit doc: ALL buttons green). Optional one amber/terracotta accent reserved only for donation tiers.
- **Buttons:** real `.btn-outline` class for the two "word-as-button" asks (white border around "donate" on Home green section; around "Support our Work" on About).
- **Photo grade:** one warm-balance/lifted-shadow recipe across all dog photos for cohesion; scrim under hero text for WCAG contrast; WebP + JPEG fallback.
- **Motion:** one ~250ms fade-up via IntersectionObserver, gated behind `prefers-reduced-motion`. Teddy video = autoplay-muted-loop-playsinline **with a visible keyboard Play/Pause** (WCAG 2.2.2); reduced-motion shows the poster.
- **Trust:** clean logo everywhere, honest "501(c)(3) in progress" language, founders named, sticky donate, favicon + OG/Twitter cards.

## Authenticity guardrails (non-negotiable)
1. **Never** generate/invent/substitute a fake dog. Only net-new pixels allowed = abstract, animal-free background textures (and even those are "cut first").
2. **Outpaint is conditional, not default** — prefer art-directed crops; if outpainting, scenery only (sky/grass/blur), cap ~15–20%, keep >70% real, reject hallucinated objects. **No outpaint on the Donate page.**
3. **Don't beautify away what the copy describes** — Nita's bio says "dirty, skin and bone"; a pristine image against that caption reads as fake. Preserve senior-dog realism (grey muzzles, cloudy eyes, scruff) — it's the brand's emotional engine.
4. **No fabricated before/after.** No medical/"cancer" framing — it appears **nowhere** in the edit doc; requires founder written confirmation.
5. **Founder sign-off before publish** on dog identity (esp. **Nita** — a blind white shepherd, easy to mis-ID, impossible to re-shoot), Pugsley's removal, any health framing.
6. **100% A/B QA per asset** vs the original; logo checked on both cream nav and green footer; eyes/fur/whiskers checked at full size for AI artifacts. Originals kept untouched (reversible).

## Credit budget
Image tools are low-credit and do most of the lift: ~12–16 image ops (1 logo chain + 4 portraits + up to 10 hero masters, fewer if cropping) + 1 video chain. Comfortably fits Higgsfield **Starter ($15/200cr)** or **Plus ($39/1000cr)** annual — no premium video-gen models, since we transcode the real `.mov` locally. `get_cost` preflight on every `upscale_image`/`outpaint`/`reframe`; batch in one session (credits expire 90 days). **Biggest savings + safety lever: crop instead of outpaint wherever the source allows.**

## Execution sequence
0. **Decisions** (below) + confirm balance via Higgsfield before any generate call.
1. **No-credit front-end first** (delivers most of the "professional" lift, zero risk): delete `contact.html` + scrub nav/footer; footer Explore/Support restructure; all brown buttons → green; the two outline "button-word" borders; Get Involved signup form + copy + delete "However You Choose to Help"; Donate email fix + remove Stripe/PayPal placeholders; favicon + OG/Twitter meta + sticky donate; build the reusable `<picture>` hero component (wired to current images until masters land).
2. **Logo pipeline** (lowest risk, highest ubiquity): upload → `remove_background` → `upscale_image(4k)` → local sips → overwrite `logo.png` everywhere → QA on cream + green.
3. **Dog portraits**: `upscale_image(2k)` → local 4:5 1080×1350 → swap Teddy/Valentino/Coffee, **delete Pugsley card, add Nita** (verbatim bio). Founder confirms identities.
4. **Heroes**: `upscale_image(4k)` → **crop** locally to 21:9 + 4:5 (outpaint only if too tight, never donate) → wire `<picture>`.
5. **Teddy video**: `upscale_video(topaz)` → optional `reframe` → ffmpeg → `<video>` with WCAG controls + poster.
6. *(optional, cuttable)* abstract textures / OG backdrop — A/B vs flat color, ship only if indistinguishable.
7. **QA + founder sign-off**, then verify live across iPhone + iPad widths.

## Open decisions (need Ryan / founders)
- **Pugsley** is deleted from the dogs cards (→ Nita). Confirm this is an endorsed placement/privacy decision, and that Nita's photo (the ~470K file) is correctly her before publish.
- **Social media URLs** (Facebook/Instagram) still never provided → keep "coming soon" placeholder, remove it, or wait?
- **Stripe/PayPal**: ship Donate with sections present but link-less (Jena adds post-launch)? (Edit doc says yes — just confirming.)
- **Higgsfield plan/credits**: confirm there's an active plan with credits before the generate steps.
- **"Teddy has cancer"** framing: do NOT use unless founders confirm in writing.
