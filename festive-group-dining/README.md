# Festive Group Dining landing page

Built 2026-09-08. Reuses the brand system extracted for `winter-events-offer/` (fonts,
tokens, nav, button styles, GTM `GTM-5KL7FBX`) rather than re-running brand extraction.
One section per venue, in the Manly Wharf Events `.split.room` idiom, per Eugene's plan.

## Venue facts (verbatim from statebuildings.com and SevenRooms, verified 2026-09-08)

| Venue | Dates | Hours | Group size | CTA |
|---|---|---|---|---|
| Long Chim | 2 Nov – 30 Dec | Tue–Sat 12PM–Late; Sun/Mon closed | 10 or more | Book Now → SevenRooms experience `4787810814836736` |
| Petition | 2 Nov – 30 Dec | Daily 12PM–10PM | 10 or more | Book Now → SevenRooms experience `6080529650597888` |
| Post | 2 Nov – 30 Dec | Lunch 12–2:30PM, dinner 5:30–9:30PM, daily | not stated | Enquire Now → `/contact` |
| Wildflower | 2 Nov – 30 Dec | Lunch Wed–Fri 12–2:30PM; dinner Tue–Sat 5:30PM–Late | 9+ for the private dining room; à la carte up to 8 | Enquire Now → `/contact` |

Contact: +61 8 6168 7888, enquiries@statebuildings.com.

## What may NOT be claimed

- **No prices are published for any festive menu.** Do not add a price without asking Emmi.
  This is a `TODO_EMAIL`: ask whether per-head pricing should appear, and if so, get figures.
- No capacity figures beyond "10 or more" (Long Chim, Petition) and "nine guests or more"
  (Wildflower PDR) / "up to eight" (Wildflower à la carte). Do not invent Post capacity.
- Menus are all "subject to change" per every source page. Keep that line on every venue.
- This is festive **group dining**, not Christmas Day dining (separate pages exist per venue
  and are out of scope) and not the general Winter Events Offer page.

## SevenRooms links

The client-supplied short links (`sevenrooms.com/x9GplWHG`, `sevenrooms.com/xBeqekmc`) carry
stale `_gl`/`_gcl_au` GA-linker params from whoever copied them. The page links to the
**resolved canonical experience URLs** instead, with no query string:
- Long Chim: `https://www.sevenrooms.com/experiences/longchim/festive-group-dining-at-long-chim-4787810814836736`
- Petition: `https://www.sevenrooms.com/experiences/petition/festive-group-dining-at-petition-6080529650597888`

Both open in a new tab (`target="_blank" rel="noopener"`) rather than an iframe, per the
[[embedded-booking-iframe-kills-meta-attribution]] rule.

## Open items to raise with the client (not build blockers)

1. **Prices** — none published anywhere. Ask Emmi.
2. **SevenRooms attribution** — a completed Long Chim/Petition booking only reaches Meta/GA4
   if SevenRooms' own Meta Pixel (`960559454688747`) and GA (`G-3P2Z4LCZ3X`) integrations are
   enabled for those two venues. Confirm with Thomas; otherwise Meta only sees the link click,
   not the booking, same gap as the Wedding Open Day Typeform issue.
3. **`/contact` thank-you** — confirm the Next.js contact form's success state lands on a URL
   containing `thank-you`, or Post/Wildflower enquiries from this page will not count toward
   the `Form Submit (URL)` custom conversion (`1759210751786952`).
4. **Google Ads** — once approved, repoint the paused Christmas Parties ad group (campaign
   `24176325511`) from `/event-type/corporate-functions` to this page, and replace the dead
   "Our Festivity" sitelink (`/festive-24`, 301s to `/whats-on`).
5. Imagery is pulled from the client's own Sanity CDN (existing published photography). Swap
   in dedicated festive photography if/when Emmi supplies it.

## Deploy

```
rsync -a clients/state-buildings/landing-pages/festive-group-dining/ clients/state-buildings/lp-site/festive-group-dining/
cd clients/state-buildings/lp-site && git add -A && git commit -m "festive-group-dining: initial build" && git push
```

Publishes at `https://lp.statebuildings.com/festive-group-dining/`. Noindex, unlinked from
any live ad — do not point traffic at it until Emmi approves copy.
