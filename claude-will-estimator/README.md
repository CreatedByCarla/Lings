# Will Cost Estimator - Lings Solicitors

Interactive 7-question tool that gives visitors an instant, no-obligation
estimate for their Will, based on the brief:

1. Who is the Will for? (single / mirror pricing)
2. Property ownership (multiple properties flagged as a complexity signal)
3. Family circumstances tick-list (children, dependants, protecting a right to live in the property)
4. How they'd like to leave their estate
5. Whether a trust might be needed (explained in plain English)
6. Complexity flags (business, overseas assets, IHT, existing trust) → routes to a bespoke quote
7. Lasting Power of Attorney cross-sell

Only **three** pricing outcomes are shown, per the brief:

| Outcome | Single | Mirror (couple) |
|---|---|---|
| Standard Will | £300 inc. VAT | £480 inc. VAT |
| Will + straightforward trust | £480–£540 inc. VAT | £720–£780 inc. VAT |
| Complex estate | "Let's talk" - bespoke fixed-fee quote | - |

The estimate is shown immediately, before any email is requested. A secondary
"Email me my estimate" CTA is included for people not ready to book - the
form in this demo is front-end only (no backend wired up yet, see below).

## Staging preview

Quick preview (Claude artifact, needs "Anyone with the link" sharing turned on
by the owner):
https://claude.ai/artifact/F4QNQ9SYjU1JY3FoekqZqY

Live GitHub Pages preview (once enabled - see below), no sign-in required:
https://createdbycarla.github.io/Lings/claude-will-estimator/

## Files

- `index.html` - fully self-contained (HTML/CSS/JS inline, Google Fonts via
  CDN, no build step, no dependencies). This is the file to embed.

## Embedding into WordPress

**Option A - Custom HTML block (simplest, recommended)**
1. Open the page/post in the WordPress block editor.
2. Add a **Custom HTML** block.
3. Paste in everything *inside* `<body>...</body>` from `index.html` (the
   `<div class="wrap">...</div>` and the `<script>` block), plus the two
   `<link>` tags and the `<style>` block from `<head>`. WordPress themes
   already provide their own `<html>/<head>/<body>`, so only the inner
   content is needed.
4. Publish and check on mobile - the widget is fully responsive.

**Option B - iframe embed (fully isolated from theme CSS, easiest to keep in sync)**
1. Upload `index.html` to the server (e.g. `/wp-content/uploads/will-estimator/index.html`),
   or host it anywhere reachable over HTTPS.
2. Add a Custom HTML block with:
   ```html
   <iframe
     src="https://www.lings-solicitors.co.uk/wp-content/uploads/will-estimator/index.html"
     style="width:100%; border:0; min-height:760px;"
     title="Will Cost Estimator"
     loading="lazy"></iframe>
   ```
3. Add a small resize script (or a fixed generous `min-height`) since the
   widget's height changes as users move through the questions - happy to
   wire up postMessage-based auto-resizing once you confirm this is the
   embed route you want.

**Option C - Code Snippets / theme plugin**
If the client uses a plugin like WPCode or Code Snippets, the same
Option A markup can be registered as a shortcode, e.g. `[will_estimator]`,
for reuse across multiple pages.

## Before this goes live (things to wire up with the client / their WordPress admin)

- **"Book your Will consultation" button** currently points to `#book-consultation`
  - needs linking to their real booking page/calendar tool.
- **"Email me my estimate"** currently only shows a front-end confirmation
  message - needs connecting to a real send (e.g. WordPress form plugin,
  Mailchimp, or a simple webhook/Zapier flow) before launch.
- **Pricing figures** are the estimator's own copy - confirm the exact fee
  bands and wording with Lings before this leaves staging (see table above).
- **Analytics** - recommend adding a GA4/GTM event on "started quiz",
  "completed quiz", "booked consultation" and "emailed estimate" once embedded.

## Brand

- Colours: `#1E4D79` (primary/navy), `#01AED6` (accent/cyan), `#ffffff`,
  `#212738` (ink)
- Fonts: Lato (headings) + Open Sans (body), loaded from Google Fonts

## Turning on the live GitHub Pages link

This repo is already pushed with everything Pages needs (a `.nojekyll` file
at the root, and this folder). One-time setup, needs repo admin access:

1. On GitHub, open **CreatedByCarla/Lings** → **Settings** → **Pages**
   (left sidebar, under "Code and automation").
2. Under **Build and deployment → Source**, choose **Deploy from a branch**.
3. Under **Branch**, select `claude/amazing-mccarthy-dk960w` and folder
   **/ (root)**, then **Save**.
4. Wait 1-2 minutes - GitHub will show a green "Your site is live at..."
   banner once it's published.
5. The estimator will be live at:
   `https://createdbycarla.github.io/Lings/claude-will-estimator/`

Every future push to this branch will redeploy automatically. Once this
work is merged into your default branch, you can point Pages at that branch
instead.
