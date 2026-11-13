# Cloudborne Mac mini rental landing page

Single static page (`index.html`, no build step, no external requests) for renting
dedicated M4 Mac minis hosted in Singapore. Chinese / English toggle; `?lang=zh|en`
forces a language. Contact is a `mailto:` link to `contact@cloudborne.cn` (constant `EMAIL`)
with a prefilled inquiry template.

- Edit copy in the `T` dictionary inside `index.html` (the `zh` and `en` blocks must
  keep the same keys). Static markup holds the Chinese text for no-JS readers.
- Competitor prices live in `RIVALS`: monthly list price of a dedicated
  M4 · 16GB · 256GB machine from each provider's own pricing page, checked 2026-11-13.
- Product photos in `assets/` are Apple's official Mac mini shots (apple.com store gallery
  and the Mac mini page's display render), cut out to transparent WebP at 1x/2x;
  `mini-hero` is the front view cropped tight for the hero reflection; `og.jpg` is the
  link-preview card (the front photo with the Cloudborne mark and name added).
- Brand: `assets/cloudborne-mark.svg` and `assets/apple-touch-icon.png` are copied unchanged
  from cloudborne.cn (`cloudborne-site` `public/favicon.svg` / `apple-touch-icon.png`); update
  them from there rather than redrawing. The footer brand links to https://cloudborne.cn.
- Layout follows a pinned "before / after" statement: `LOG` holds the illustrative
  connection rows (documentation-range IPs, RFC 5737). The rows flip as the section
  scrolls; the hub wires between the Mac mini and the four windows are drawn in JS.
- Preview: open `index.html` in a browser, or `python3 -m http.server` in this folder.
- Deploy: public repo `Jaaay50/cloudborne-mac-mini`, GitHub Pages from `main` / root
  (`.nojekyll` is present); a push to `main` is live in about a minute at
  https://mac.cloudborne.cn/ (custom domain from the `CNAME` file; DNSPod `mac` CNAME →
  `jaaay50.github.io.`, HTTPS enforced). The github.io address redirects there. If the domain
  changes, update `CNAME` plus `og:url` and `og:image` in `index.html`.
