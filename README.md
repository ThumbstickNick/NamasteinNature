# Namaste in Nature

A modern, hand-coded rebuild of [namasteinnature.com](https://namasteinnature.com) — guided outdoor wellness (Micro Retreats™, yoga, sound healing, mobile massage) in Asheville, NC.

## Tech

- Static HTML5 + modern CSS (design tokens via custom properties) + vanilla JS. No build step.
- Mobile-first, responsive, accessible; respects `prefers-reduced-motion`.
- Booking via embedded **Peek Pro** widgets (added in a later phase).
- Structured for portability to a WordPress theme later (shared header/footer, semantic sections, token-based CSS).

## Structure

```
index.html            Home page
assets/css/styles.css Design tokens + all styles (re-theme via :root)
assets/js/main.js     Mobile nav, scroll-reveal, footer year
assets/img/           Photography (imported in the media pass)
partials/             Reference markup for shared header/footer (WP port)
blog/                 Blog index + posts
```

## Run locally

```
python -m http.server 5500
```

Then open http://localhost:5500 — paths are relative, so it also works from a GitHub Pages project subpath.

## Roadmap

1. Scaffold — structure, CSS tokens, header/footer + mobile nav, Home hero (done)
2. Service pages (Micro Retreats, Yoga, Sound Healing, Mobile Massage, Gift Cards)
3. Supporting pages (Team, FAQ, Contact + booking, Blog)
4. Media pass — import & optimize photos from the current site
5. Polish — animations, SEO/OpenGraph, a11y, performance, 404
6. Deploy to GitHub Pages
