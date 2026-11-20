# Cloudborne Mac mini rental landing page

Single static page (`index.html`, no build step, no external requests) for renting
dedicated M4 Mac minis hosted in Singapore with optional Claude Team Premium seats.
Chinese / English toggle; `?lang=zh|en` forces a language. Contact is a `mailto:` link
to `contact@cloudborne.cn` (constant `EMAIL`) with prefilled inquiry templates.

- Edit copy in the `T` dictionary inside `index.html` (the `zh` and `en` blocks must
  keep the same keys). Static markup holds the Chinese text for no-JS readers.
- Competitor prices live in `RIVALS`: monthly list price of a dedicated
  M4 · 16GB · 256GB pure-hardware machine from each provider's own pricing page, checked
  2026-11-13. Do not compare bundled seat pricing against hardware-only competitors.
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
- Pricing (`PLANS` & `SEAT`):
  - `PLANS` drives pure Mac pricing (`m`: $99/mo, `q`: $267/qtr upfront eq. $89/mo,
    `y`: $948/yr upfront eq. $79/mo). Quarterly (-10%) and yearly (-20%) discounts apply
    to Mac hardware only.
  - `SEAT` holds `mo: 299` ($299/seat/mo, Cloudborne service price, excl. Mac rental,
    `standaloneAllowed: false`). Bundle pricing (`m`: $398/mo, `q`: $1,164/qtr upfront eq.
    $388/mo, `y`: $4,536/yr upfront eq. $378/mo) stays synchronized via `#cyc` and `#cycB`.
  - All storefront prices are listed in USD excl. tax, with settlement accepted in USD or
    equivalent CNY. Update `meta` / `og` descriptions and `T` copy together if pricing changes.
- Preview: open `index.html` in a browser, or `python3 -m http.server` in this folder.
- Deploy: public repo `Jaaay50/cloudborne-mac-mini`, GitHub Pages from `main` / root
  (`.nojekyll` is present); a push to `main` is live in about a minute at
  https://mac.cloudborne.cn/ (custom domain from the `CNAME` file; DNSPod `mac` CNAME →
  `jaaay50.github.io.`, HTTPS enforced). The github.io address redirects there. If the domain
  changes, update `CNAME` plus `og:url` and `og:image` in `index.html`.

## Acceptance before and after a push

Check with headless Chrome (Playwright) at 1440, 1024, 390 and 360 px, in Chinese and English:
no horizontal scroll and no console errors; `T.zh` and `T.en` have the same keys; each
billing period updates both `#plan-mac` and `#plan-bundle` with monthly equivalent and
upfront total and lands in the `mailto:` body; every `.js-mail` link starts with
`mailto:contact@cloudborne.cn`; the copy-email button works. After a push, wait for the
Pages build (`gh api repos/Jaaay50/cloudborne-mac-mini/pages/builds/latest`), then confirm
the live `index.html` is byte-identical to the local file.
