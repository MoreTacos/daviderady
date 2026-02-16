# daviderady.com

Personal website of Davide Radaelli. Pure static HTML/CSS, no build tools or frameworks.

## Tech Stack

- Vanilla HTML5 + CSS3 (single `style.css`, ~370 lines)
- No JavaScript frameworks — only minimal vanilla JS for service worker cleanup and speculation rules
- Fonts: Chivo (headings), Open Sans (body) — self-hosted WOFF2 in `/fonts/`
- Hosted on **Cloudflare Pages** — deploys automatically on `git push` to `main`

## Project Structure

```
/                          # Site root
├── index.html             # Homepage
├── style.css              # Global stylesheet (also inlined in every page <style>)
├── blog/index.html        # Blog listing
├── now/index.html         # "Now" page
├── math/index.html        # Math/letter page
├── posts/{slug}/index.html  # 15 blog posts (each in own directory)
├── fonts/                 # WOFF2 web fonts
├── images/                # Profile + post images (WebP preferred, JPG fallback)
├── _redirects             # Cloudflare Pages redirects (www→non-www + old WordPress URLs)
├── _headers               # Cloudflare Pages security headers (CSP, HSTS, etc.)
├── sitemap.xml            # XML sitemap for search engines
├── robots.txt             # Allow all + sitemap reference
└── google894064f07f4ba773.html  # Search Console verification
```

## Key Conventions

- **CSS is inlined**: Every HTML page has the full stylesheet in a `<style>` tag (not linked externally). When updating `style.css`, you must also update the inlined CSS in every page.
- **Content width**: 720px (`--content-width`)
- **Responsive breakpoint**: 600px
- **Date format**: "Month Day, Year" (e.g., "January 17, 2022")
- **Title format**: `[Post Title] – Davide Radaelli`
- **Images**: Include `width`/`height` attributes; use `fetchpriority="high"` on first image

## Adding a New Blog Post

1. Create `/posts/{slug}/index.html` — copy template from any existing post
2. Update: `<title>`, `<meta description>`, `<link rel="canonical">`, `<h1>`, `<p class="meta">` date
3. Write content inside `<div class="page-body">` using standard HTML
4. Add entry to `/blog/index.html` (top of `.blog-list` ul)
5. Add `<url>` entry to `/sitemap.xml`

## Config Files

- **`_redirects`**: Cloudflare redirect rules. 301s from old WordPress date-based URLs to new `/posts/` paths.
- **`_headers`**: Security headers (CSP, HSTS, X-Frame-Options, etc.) applied to all routes.
- **`sitemap.xml`**: Priorities: 1.0 (home), 0.9 (blog), 0.8 (now), 0.7 (posts)

## CSS Variables

```css
--color-primary: #000000
--color-secondary: #007cba        /* links, accents */
--color-foreground: #333333
--color-background: #FFFFFF
--font-heading: Chivo, "Playfair Display", Georgia, serif
--font-body: "Open Sans", "Fira Sans", Helvetica, Arial, sans-serif
--content-width: 720px
```

## Commit Style

Imperative, concise, one line: `Add ...`, `Fix ...`, `Update ...`, `Change ...`

## Deployment

Push to `main` → Cloudflare Pages auto-deploys. No build step.
