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


## Client feedback round 1 (Emmi, 2026-09-09) - APPLIED

Emmi approved the page in principle ("lovely job") and asked for six changes "to align with
our new brand guidelines". All six applied and redeployed 2026-09-09:

| # | Request | What was done |
|---|---|---|
| 1 | "4 restaurants, one precinct" -> "one building", set in Times New Roman | Copy changed; `.hero__proof` switched from Dada Grotesk to `--font-serif` |
| 2 | Months written in full | "2 Nov - 30 Dec" -> "2 November - 30 December". No other abbreviations existed |
| 3 | Venue days & hours in Times New Roman | `.venue__meta` switched to `--font-serif` |
| 4 | Background white -> cream `#F0EEDE` | Added `--cream`; applied to `body`, the previously-sand sections and the footer |
| 5 | Footer phone/email in Times New Roman | `.enquire__contact` switched to `--font-serif` (the actual `<footer>` was already serif) |
| 6 | Buttons to ~60% "to match SB button sizing" | Matched the real site spec, not a guess (see below) |

**On the button sizing.** statebuildings.com renders its buttons with
`font-button flex h-8 items-center justify-center gap-2 rounded-full bg-black px-3 py-2 text-xs tracking-[0.5px] text-white uppercase`.
That is: 32px fixed height, 0.75rem/0.5rem padding, 0.75rem type, 0.5px tracking. Our button
was ~52px tall, so the site's is 61% of it - which is exactly the "~60%" Emmi asked for. The
`.btn` base rule lives in the SHARED `css/style.css` (used by winter-events-offer too), so the
override is in this page's inline `<style>` block. Do not "fix" it in the shared file.

**Judgement call worth flagging to Emmi.** The request was "background white to cream". The
page also had lightly-tinted sand sections (`#f7f7ef`) alternating with white. Cream `#F0EEDE`
is *darker* than that sand, so leaving sand as-is would have made those bands read as lighter
patches on the cream. They were unified to the same cream and delineated with hairline rules
instead. If the new brand guidelines include a second background tone, that is the value to
drop into `--sand`.

**Still with the client.** Their designer was shifting content the following day and sending it
back; Emmi is also confirming all headings/copy and wants to discuss launching Google Ads at
the same time. Expect a round 2 - do not treat the current copy as final.

## Client feedback round 2 (Emmi, 2026-09-11) - APPLIED

Emmi forwarded two small change requests, quoted alongside two lines she was just confirming
were already correct (no action needed on those):

| # | Request | What was done |
|---|---|---|
| 1 | "4 restaurants" -> "Four Restaurants, One Building" for consistency | `.hero__proof` changed from `<strong>4</strong> restaurants, one building` to `<strong>Four</strong> Restaurants, One Building`, matching the section heading "Four Restaurants, One Festive Season" |
| 2 | Petition trading hours: main Petition page lists until 9pm | `.venue__meta` for Petition changed from `12PM–10PM` to `12PM–9PM` |

The other two quoted lines (the hero intro sentence and the Wildflower PDR note) already
matched the page verbatim - no change made, treated as confirmation not a request.

**Note for next round hours audit.** Long Chim's listed hours (`Tue–Sat 12PM–Late`) were not
raised by Emmi this time and were left as-is, but given Petition's hours had drifted from the
live site, it may be worth asking her to confirm Long Chim and Post/Wildflower hours too next
time she reviews, rather than waiting for her to catch each one individually.

## Deploy

```
rsync -a clients/state-buildings/landing-pages/festive-group-dining/ clients/state-buildings/lp-site/festive-group-dining/
cd clients/state-buildings/lp-site && git add -A && git commit -m "festive-group-dining: initial build" && git push
```

Publishes at `https://lp.statebuildings.com/festive-group-dining/`. Noindex, unlinked from
any live ad — do not point traffic at it until Emmi approves copy.
