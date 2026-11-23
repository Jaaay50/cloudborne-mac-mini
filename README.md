# Cloudborne Mac mini rental landing page

Single static page (`index.html`, no build step, no external requests) for renting
dedicated M4 Mac minis hosted in Singapore with optional Claude Team seats (Standard or Premium).
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
- Pricing (`PLANS`, `SEATS` & `SEAT_POLICY`):
  - `PLANS` drives pure Mac pricing (`m`: $99/mo, `q`: $267/qtr upfront eq. $89/mo,
    `y`: $948/yr upfront eq. $79/mo). Quarterly (-10%) and yearly (-20%) discounts apply
    to Mac hardware only. Pure Mac rentals require **$0 deposit**.
  - `SEATS` holds `std.mo: 50` ($50/seat/mo, Cloudborne service price, bundled with Mac
    for $149/mo) and `prem.mo: 299` ($299/seat/mo, Cloudborne service price, bundled with
    Mac for $398/mo); `SEAT_POLICY` sets `standaloneAllowed: false` and `depositPct: 30`.
    Every bundle/subscription plan charges a refundable 30% deposit calculated on the
    upfront period total and rounded to whole USD:
    - Standard bundle: `m` $45 on $149 → $194 first total; `q` $125 on $417 → $542 first
      total; `y` $464 on $1,548 → $2,012 first total.
    - Premium bundle: `m` $119 on $398 → $517 first total; `q` $349 on $1,164 → $1,513
      first total; `y` $1,361 on $4,536 → $5,897 first total.
    Refunded in full on normal cancellation/term end; seat violations (off-Mac login,
    Claude Code reverse-proxying/token export, seat sharing, automated farming/scraping)
    result in immediate termination of both the seat and the paired Mac with no refund of
    rent or deposit. Cycles synchronize via `#cyc` and `#cycB`; seat tiers synchronize
    via `#tierS` and `#tierB`.
  - `#rules` documents the paired-Mac login restriction, anti-proxy/anti-sharing/anti-abuse
    seat rules, Mac hardware/network AUP (no mining, attacks, public proxies, sub-leasing),
    and the joint seat+Mac termination and forfeiture enforcement policy.
  - All storefront prices are listed in USD excl. tax, with settlement accepted in USD or
    equivalent CNY. Update `meta` / `og` descriptions and `T` copy together if pricing changes.
- Preview: open `index.html` in a browser, or `python3 -m http.server` in this folder.
- Unlisted private time-sharing guide (`split/index.html` → `https://mac.cloudborne.cn/split`):
  intentionally unlinked from the main storefront and marked `<meta name="robots" content="noindex, nofollow, noarchive">`.
  Presents the reference split math for a single full Premium bundle ($398/mo, ~$2,880 CNY + 30%
  refundable deposit $119, ~$860 CNY) across 4 / 3 / 2 time-shifted users (1 concurrent remote user
  on the physical Mac, group self-organized with 1 designated settlement contact and joint red-line
  enforcement). Do not link it from `index.html` or list it in `robots.txt`.
- Deploy: public repo `Jaaay50/cloudborne-mac-mini`, GitHub Pages from `main` / root
  (`.nojekyll` is present); a push to `main` is live in about a minute at
  https://mac.cloudborne.cn/ (custom domain from the `CNAME` file; DNSPod `mac` CNAME →
  `jaaay50.github.io.`, HTTPS enforced). The github.io address redirects there. If the domain
  changes, update `CNAME` plus `og:url` and `og:image` in `index.html`.

## Acceptance before and after a push

Check with headless Chrome (Playwright) at 1440, 1024, 390 and 360 px, in Chinese and English:
no horizontal scroll and no console errors; `T.zh` and `T.en` have the same keys; each
billing period and seat tier (`std` / `prem`) updates `#plan-mac`, `#plan-seat`, and
`#plan-bundle` with monthly equivalent, upfront total, and deposit, and lands in the
`mailto:` body; every `.js-mail` link starts with `mailto:contact@cloudborne.cn`; the
copy-email button works. After a push, wait for the Pages build
(`gh api repos/Jaaay50/cloudborne-mac-mini/pages/builds/latest`), then confirm the live
`index.html` is byte-identical to the local file.
