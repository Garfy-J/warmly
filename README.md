# Warmly

Screen candidates against a JD and send every applicant a warm, personal reply. Phone-first, free, no sign-up.

- Paste a JD or pick a template, then add CVs (PDF, Word or text).
- Each requirement is checked against each CV, with the matching line shown as evidence.
- Flags potential (promotions, built from zero, led a team, quantified results, cross-market work).
- Drafts a reply for each candidate: interview, keep warm or kind decline; warm, friendly or formal; English or 中文.
- Runs entirely in the browser. CVs are never uploaded. PDF and Word files are read with pdf.js and mammoth, loaded from jsDelivr only when a file is added.

## Files
- `public/index.html`: the whole app (HTML, CSS and JavaScript in one file), with SEO meta, Open Graph, and JSON-LD for WebApplication, FAQPage and HowTo
- `public/og.png`: the share image (1200×630)
- `public/llms.txt`, `public/robots.txt`, `public/sitemap.xml`: for search engines and AI answer engines
- `wrangler.jsonc`: Cloudflare config, serves `public/` as static files

## Live hosting (Cloudflare Workers)
The site deploys automatically from the `main` branch. Cloudflare runs `npx wrangler deploy`, which publishes the `public` folder as set in `wrangler.jsonc`. There is no build step. Push to `main` and the site updates within a few minutes.

## Run locally
Open `public/index.html` in a browser, or run `npx serve public`.

## Known limits
- Matching is rule-based (keywords, synonyms, years of experience), not AI, so it's a first pass.
- Google Fonts and jsDelivr can be slow or blocked in mainland China. The page falls back to system fonts, but PDF and Word reading need jsDelivr. Pasting CV text always works.

## Sending from Gmail or Outlook
Direct sending is off until OAuth client IDs are added to `MAILCFG` near the "send from your inbox" section of `public/index.html`. With both left empty, the Settings section is hidden and replies can still be copied or opened in Gmail, Outlook or a mail app. Tokens stay in the browser; Warmly asks only for permission to send, never to read mail.

**Gmail (Google Cloud, free)**
1. Create a project at console.cloud.google.com and enable the Gmail API.
2. OAuth consent screen: External, app name Warmly, add the scope `https://www.googleapis.com/auth/gmail.send`.
3. Credentials → Create OAuth client ID → Web application. Authorised JavaScript origin: `https://warmly.garfy.workers.dev` (and any custom domain).
4. Put the client ID in `MAILCFG.google`.
While the app is in Testing mode, only the test users you add (up to 100) can connect. `gmail.send` is a sensitive scope, so making it public needs Google's verification.

**Outlook (Microsoft Entra, free)**
1. portal.azure.com → App registrations → New registration. Supported accounts: any organisational directory plus personal Microsoft accounts.
2. Add a Single-page application redirect URI: `https://warmly.garfy.workers.dev/`.
3. API permissions → Microsoft Graph → Delegated → `Mail.Send` and `User.Read`.
4. Put the Application (client) ID in `MAILCFG.microsoft`.
Some company tenants require an admin to approve new apps before staff can connect.

When direct sending is switched on, also update the "own Gmail or Outlook" FAQ answer, the JSON-LD featureList and FAQ in `index.html`, and `llms.txt`, so they say replies can be sent without leaving Warmly.
