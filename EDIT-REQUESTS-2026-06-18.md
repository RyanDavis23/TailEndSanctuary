# Tail End Sanctuary — Edit Requests (June 18, 2026 batch)

**Source:** 8 page-by-page emails from Juanita Crampton (`juanitacrampton@gmail.com`, logo email from `ajijicburros108@icloud.com`), sent June 18 2026, forwarded by Ryan's agent June 21. Cross-referenced against the agent's June 11 status email.

**Recipients/owners:** Juanita Crampton · Ronni Coppola (`coppolaryan@aol.com`) · Jena Marie Olio (`jena@clickerpets.com.mx`)
**Confirmed contact email for the site:** `info@tailendsanctuary.org`

---

## GLOBAL — applies to every page

- [ ] **Replace the logo** in the header on all pages. New clean file attached to the "Logo" email: **`Tailend Logo.png`**. (Resolves the agent's June 11 open item — they had no clean logo before; now they do.) A ChatGPT reference link was also included.
- [ ] **Replace the footer logo** on all pages (called out on every page + the Footer email).
- [ ] **Hero image responsive fix (site-wide).** Every page's hero "formats well on iPhone but not iPad" (or vice-versa). iPhone consistently "shows more of the photo / more depth." The hero images crop inconsistently across devices — fix the responsive cropping so heroes display consistently on phone *and* tablet.
- [ ] **Button color consistency:** all call-to-action buttons should be **green** (matching the Donate button). Brown buttons get changed to green (specifically flagged on Home + Meet the Dogs).

---

## HOME — `index.html`
- [ ] Change logo (header).
- [ ] **Hero:** formats well on iPad, **not** iPhone. Replace hero photo with attached → `6d5b08bf-2d10-443a-9d0e-aab94116c2f2.jpeg`.
- [ ] **Hero:** delete the two buttons ("Give Them a Peaceful Ending" / "Meet the Dogs").
- [ ] **"Meet Teddy" section:** delete Teddy photo, replace with the **Teddy video** → `ced729ab-9f87-425e-9780-ec60b899a120.mov`.
- [ ] **"Meet Teddy" button:** change from brown → green (match Donate).
- [ ] **Last green section ("You can give…"):** add a white outline/border around the word **"donate"** so it reads as an actual button.
- [ ] Footer: change logo.

## ABOUT US — `about.html`
- [ ] Change logo (header).
- [ ] **Hero:** formats well on iPhone, **not** iPad. Replace photo with **Cindy** → `f9c47d9e-448e-4941-996d-06eed8eab1f1.jpeg`.
- [ ] **"Be Part of This Work" section:** add a white border around **"Support our Work"** to make it a button.
- [ ] Footer: change logo.

## MEET THE DOGS — `dogs.html`
- [ ] Change logo (header).
- [ ] **Hero:** formatting not as good on iPad as iPhone (covered by global hero fix).
- [ ] **Change Teddy photo** → new (≈266K).
- [ ] **Delete Pugsley** (photo + bio) → **replace with Nita** (new photo ≈470K + new bio below).
- [ ] **Change Valentino photo** → new (≈147K).
- [ ] **Change Coffee photo** → new (≈171K).
- [ ] Change the "Help a dog like…" buttons brown → green.
- [ ] Footer: change logo.

**Nita bio (new copy, verbatim):**
> Nita was found late one night in Ajijic. She was obviously blind and unaware she was lying in the middle of the street. A kind neighbor led this beautiful white shepherd to safety for the night. Nita was dirty, skin and bone and truly lost. The following day Nita was taken to the vet then directly to Tail End Sanctuary where she was welcomed and cared for with great love and devotion.

**4 photos attached** (filenames are random; match to dog by file size):
`5da66abe-3a2a-4090-979f-e5bb768ae51a.jpeg`, `IMG_2825.jpeg`, `att.RYJGY5B3xgUntSSWEwZ8NrU_nJm5AfAYTOnhVLFHAww.jpeg`, `01a7edb8-5ac9-4a89-b36c-af53d4f072ab.jpeg`
Stated order/sizes → **Teddy 266K · Nita 470K · Valentino 147K · Coffee 171K.**

## GET INVOLVED — `get-involved.html`
- [ ] Change logo (header).
- [ ] **Hero:** iPad/iPhone formatting (global fix). Replace photo with **Senta** → `84d4ed8d-4cfc-43a1-9d07-b9d299aa0c46.jpeg`.
- [ ] **"Stay in Touch" section:** change text to → *"Stay connected for updates on the sanctuary and our dogs."*
- [ ] **"Stay in Touch":** embed a **simple email signup form directly on the page** (so people don't have to leave the page).
- [ ] **Delete the section "However You Choose to Help."**
- [ ] Footer: change logo.

## CONTACT — `contact.html`
- [ ] **DELETE the Contact page entirely.** Reason (Juanita): no staff to reply to messages; the email address is already in the footer of every page. → Also remove Contact from the nav + footer. Confirmed email: `info@tailendsanctuary.org`.

## DONATE — `donate.html`
- [ ] Change logo (header).
- [ ] **Hero:** iPad/iPhone formatting (global fix). Replace hero photo with attached → `1b30b24a-5bad-40cc-ae33-4635f6c18241.jpeg`.
- [ ] **Bank of America section:** change email to `info@tailendsanctuary.org`.
- [ ] **Stripe + PayPal sections:** keep the sections, **delete the placeholder link info**. Jena will add the correct 501(c)(3) links *once the site is live* (she can't generate them until then).
- [ ] Footer: change logo.

## FOOTER — global component (every page)
- [ ] Change logo (noted per-page).
- [ ] Under heading **"Explore"** → list: Home, About Us, Meet the Dogs.
- [ ] Rename heading **"Get Involved" → "Support"**; under Support → list: Get Involved, Donate.
- [ ] (Implied) Drop the Contact link, since the Contact page is being deleted.

---

## STILL OPEN / NEEDS INPUT
- [ ] **Social media links** — the agent added a "Social Links Coming Soon" placeholder on June 11. The founders have **not yet sent** the actual Facebook/Instagram URLs. → Need the links, or decide to keep the placeholder / remove it.
- [ ] **Stripe + PayPal donation links** — intentionally deferred by Jena until the site is live.
- [ ] **Teddy "cream/color" Photoshop edit** (from the April thread, left to Jena) — likely moot now that Teddy gets a new photo + video, but worth a one-line confirm.

## TECH NOTES (for implementation)
- The Teddy file is a **`.mov`** — will likely need conversion to **`.mp4`** (H.264) + a poster image for reliable in-browser playback.
- Several incoming photos are large phone images — resize/compress for web before committing.
- Photos/videos are **email attachments** that still need to be extracted from Gmail into `images/` before edits can be made.
