# Warmly

Screen candidates against a JD and send every applicant a warm, personal reply. Phone-first, free, no sign-up.

- Paste a JD or pick a template, then add CVs (PDF, Word or text).
- Each requirement is checked against each CV, with the matching line shown as evidence.
- Flags potential (promotions, built from zero, led a team, quantified results, cross-market work).
- Drafts a reply for each candidate: interview, keep warm or kind decline; warm, friendly or formal; English or 中文.
- Runs entirely in the browser. CVs are never uploaded. PDF and Word files are read with pdf.js and mammoth, loaded from jsDelivr only when a file is added.

## Files
- `public/index.html`: the whole app (HTML, CSS and JavaScript in one file)
- `wrangler.jsonc`: Cloudflare config, serves `public/` as static files

## Live hosting (Cloudflare Workers)
The site deploys automatically from the `main` branch. Cloudflare runs `npx wrangler deploy`, which publishes the `public` folder as set in `wrangler.jsonc`. There is no build step. Push to `main` and the site updates within a few minutes.

## Run locally
Open `public/index.html` in a browser, or run `npx serve public`.

## Known limits
- Matching is rule-based (keywords, synonyms, years of experience), not AI, so it's a first pass.
- Google Fonts and jsDelivr can be slow or blocked in mainland China. The page falls back to system fonts, but PDF and Word reading need jsDelivr. Pasting CV text always works.
