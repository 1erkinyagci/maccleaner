# MacCleaner — Landing Site

Marketing/landing site for **MacCleaner**, the trust-first AI storage assistant for Mac.
Static HTML/CSS (no build step) served from this repo.

Live: **https://maccleaner.io** (Vercel, custom domain). The `1erkinyagci.github.io/maccleaner/` mirror still serves the same repo; every page canonicalises to maccleaner.io.

## What's here

| File | Purpose |
| --- | --- |
| `index.html` | The landing page (hero, how-it-works, coverage, pricing, FAQ). |
| `blog/` | 10 storage guides + `blog/index.html`. Hero art in `blog/img/`. |
| `blog.css` | Shared blog stylesheet — mirrors the landing's `:root` tokens. |
| `success.html` | Post-checkout success page (Stripe `success_url`). |
| `cancel.html` | Checkout-cancelled page (Stripe `cancel_url`). |
| `og.png` | Open Graph / Twitter social share image (1200×669). |
| `sitemap.xml`, `robots.txt` | SEO. `robots.txt` also names the AI crawlers. |
| `llms.txt` | Short factual summary for AI answer engines. |
| `google*.html` | Google Search Console verification. |
| `.nojekyll` | Tells GitHub Pages to serve files as-is (no Jekyll build). |

## Deployment

Every push to `master` deploys automatically:

- **GitHub Pages** — repo `1erkinyagci/maccleaner`, branch `master`, source = repo root.
- **Vercel** — project `maccleaner`, connected to this repo (production = `master`).

```bash
# edit the HTML, then:
git add index.html cancel.html success.html
git commit -m "Landing: <what changed>"
git push origin master
# live in ~1 min on both Pages and Vercel
```

No install, no build — just edit the HTML and push.

## Positioning (keep in sync with the app)

The copy must match the shipped app:

- **Story:** scan read-only → see what's *safely recoverable* → **Scout** (the built-in AI helper) explains everything → you choose Trash or permanent. Nothing is ever deleted automatically.
- **Pricing:** Free = up to **500 MB of cleanup per day** (scanning + Scout always free/unlimited); Pro = unlimited cleanup — $4.99/mo, $19.99/yr, $29.99 lifetime.
- **Download** links point at the latest GitHub Release DMG (currently `v0.1.13`). Update them in `index.html` + `success.html` when a new version ships — and the `softwareVersion` / `downloadUrl` in the `SoftwareApplication` JSON-LD too.

## Adding a blog post

Every post is standalone HTML — copy an existing one and edit. Keep these, or the
post loses its SEO value:

- `<link rel="canonical">`, OG/Twitter tags, and a unique `<title>` + meta description.
- The three JSON-LD blocks: `BlogPosting`, `BreadcrumbList`, `FAQPage`.
- The `.answer` box up top — a short, self-contained answer. This is what AI
  engines quote, so it has to stand on its own without the rest of the page.
- A new `<url>` entry in `sitemap.xml`, and a card in `blog/index.html`.

**No third-party trademarks in the art.** The generated illustrations must not
carry Apple's logo (or anyone else's) — check the monitor bezel/chin before
shipping, image models add it unprompted.

Claims must match the shipped app. Free = 500 MB/day, cleanups go to
MacCleaner's own recoverable area (not Finder's Trash), nothing auto-deletes.

## Related

- **App source:** `1erkinyagci/maccleaner-app` (React + Vite + Electron; not this repo).
- **Checkout:** the pricing buttons call the Supabase `create-checkout` edge function → Stripe Checkout; `stripe-webhook` activates the license. Analytics via GA4 (`G-RNNJD0Q0RB`).
