# SEO Migration Plan — Squarespace → static site

Goal: move `namasteinnature.com` from Squarespace to this hand-coded site
**without losing rankings or backlinks.** The platform change is invisible to
Google; what matters is that URLs, content signals, and the domain carry over.

---

## 1. URL redirect map

The new site uses `.html` filenames. Squarespace used extension-less slugs.
**Confirm each "Old URL" against your live Squarespace nav / Search Console
before launch** — the right column is the canonical target on the new site.

| Old Squarespace URL (verify)            | New URL                                   | Action  |
|-----------------------------------------|-------------------------------------------|---------|
| `/`                                     | `/`                                       | same    |
| `/micro-retreats`                       | `/micro-retreats.html`                    | 301     |
| `/yoga`                                 | `/yoga.html`                              | 301     |
| `/sound-healing`                        | `/sound-healing.html`                     | 301     |
| `/mobile-massage`                       | `/mobile-massage.html`                    | 301     |
| `/gift-cards`                           | `/gift-cards.html`                        | 301     |
| `/team` (or `/about`)                   | `/team.html`                              | 301     |
| `/faq`                                  | `/faq.html`                              | 301     |
| `/contact` (or `/book`, `/booking`)     | `/contact.html`                           | 301     |
| `/blog`                                 | `/blog/index.html`                        | 301     |
| `/blog/<post-slug>`                     | `/blog/<post-slug>.html`                  | 301 ea. |

### How to find the *real* old URLs
1. Google Search Console → **Pages** report → export the indexed URL list.
2. Or `https://namasteinnature.com/sitemap.xml` (Squarespace auto-generates one)
   — copy every `<loc>` before you cut over.
3. Map each one to a new page above. Anything with no equivalent → redirect to
   the closest page or the homepage (never let it 404).

### Important: redirects need the right host
- **GitHub Pages cannot do server-side 301 redirects.** It only supports
  client-side meta-refresh/JS, which passes link equity weakly.
- Options, best to worst for SEO:
  1. **Match URLs exactly** (drop `.html` via a host that allows it) — no
     redirects needed.
  2. Move the live domain to **Cloudflare Pages / Netlify** (free, real 301s +
     a `_redirects` file).
  3. Stay on GitHub Pages and accept client-side redirects for changed slugs.
- Easiest high-value win: keep the homepage and don't change slugs you don't
  have to.

---

## 2. Pre-launch checklist (already done in this repo)
- [x] `sitemap.xml` at site root (lists all 11 pages, apex domain).
- [x] `robots.txt` at site root, references the sitemap.
- [x] `<link rel="canonical">` on every page → apex `namasteinnature.com`.
  (On the github.io staging host the canonical still points at production, which
  *reduces* duplicate-content risk.)
- [x] Staging `noindex`: `assets/js/main.js` injects
  `<meta name="robots" content="noindex,nofollow">` **only** when the host ends
  in `.github.io`. The live domain is never noindexed.
- [x] `LocalBusiness` (HealthAndBeautyBusiness) JSON-LD on the homepage:
  name, phone `(828) 276-3536`, Asheville NC, geo, logo, social `sameAs`.
- [x] Per-page `<title>` + `<meta name="description">` carried over / improved.
- [x] Descriptive `alt` text on images; lazy-loading below the fold.

## 3. Decide before cutover
- [ ] **www vs apex.** This repo standardizes on apex `namasteinnature.com`.
  Pick one as canonical and 301 the other (host-level). Update the canonical
  tags + sitemap if you choose `www`.
- [ ] **Hosting for the live domain** (see redirect note in §1).
- [ ] Real social URLs in the footer + JSON-LD `sameAs` (currently placeholders).

## 4. Launch day
1. Point DNS / domain to the new host.
2. Confirm `https://namasteinnature.com/robots.txt` and `/sitemap.xml` load.
3. Spot-check 5–10 old URLs → confirm they 301 to the right new page.
4. View-source a couple of live pages → confirm **no** `noindex` tag is present
   (it should only appear on github.io).

## 5. After launch (Google Search Console)
1. Verify ownership of the domain (re-verify if it was tied to Squarespace).
2. Submit `https://namasteinnature.com/sitemap.xml`.
3. Use **URL Inspection → Request indexing** on the homepage + top pages.
4. Watch **Pages** (coverage) and **Performance** for ~4 weeks. A small,
   temporary ranking dip during recrawl is normal; it recovers.
5. Keep the Squarespace site's old sitemap reachable until Google has processed
   the redirects (helps it discover the moves faster).
