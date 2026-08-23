# statebuildings-lp

Static landing pages for State Buildings, served by GitHub Pages at **https://lp.statebuildings.com**.

Built by Merge Digital Marketing with `/full-landing-page-builder`. Source-of-truth packages live in the agency workspace at `clients/state-buildings/landing-pages/<slug>/`; this repo holds the deployed copy.

## Layout

```
CNAME            lp.statebuildings.com (never delete: dropping it resets the custom domain and loses the cert)
.nojekyll        serve files raw, no Jekyll build
robots.txt       Disallow all. Paid landing pages are noindex to avoid duplicate content against statebuildings.com
index.html       holding page (noindex)
<slug>/          one folder per landing page: index.html, css/, fonts/, images/, thank-you/index.html
```

## Deploy

```
cp -R clients/state-buildings/landing-pages/<slug>/ lp-site/<slug>/
mv lp-site/<slug>/thanks.html lp-site/<slug>/thank-you/index.html   # thank-you URL must contain "thank-you"
git add -A && git commit -m "<slug>: ..." && git push
```
Pages publishes from `main` `/` within about a minute. Verify: `curl -sI https://lp.statebuildings.com/<slug>/`.

## DNS (client side, Route 53)

`lp.statebuildings.com  CNAME  mrgmarketing781.github.io.`

## Tracking

Every page loads GTM `GTM-5KL7FBX` (same container as statebuildings.com), so the Meta pixel `960559454688747` and GA4 `G-3P2Z4LCZ3X` fire without new tags. Enquiry forms are Typeform embeds that redirect on completion to `/<slug>/thank-you/`, which fires the existing Meta custom conversion `Form Submit (URL)` (URL contains `thank-you`). `lp.statebuildings.com` must be on the GA4 cross-domain list.
