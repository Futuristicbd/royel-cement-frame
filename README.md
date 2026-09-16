# Royal Cement Campaign Studio

A small, dependency-free photo frame platform deployed on Vercel. Public campaign pages and a separate authenticated admin panel.

## Visitors

- Browse published campaigns and share `/c/<slug>` links.
- Upload JPG, PNG or WebP photos (max 20 MB). Photos stay in the browser.
- Drag, pinch, zoom, rotate 90 degrees, reset, or use arrow keys to reposition.
- Choose among up to six campaign frames.
- Download a 1080 × 1080 PNG without watermarks.
- Copy the campaign caption or download and copy in one click.

## Admin

Visit `/admin`. Sign in using a **fine-grained GitHub personal access token** belonging to an account with write access to this repository:

1. Open https://github.com/settings/personal-access-tokens/new
2. Choose resource owner **Futuristicbd** and **Only select repositories → royel-cement-frame**.
3. Set **Repository permissions → Contents → Read and write**. No other additional permission is needed.
4. Choose a suitable expiration, generate, and paste it into the admin sign-in form. Do not share the token or put it in a caption, source code, or campaign link.

The token is held only in JavaScript memory; it is not written to localStorage, sessionStorage, cookies, the repository, or a third-party server. Requests with the token go only to GitHub's repository API. Closing/reloading the tab signs you out. GitHub enforces write permission on every save. This intentionally uses repository-backed admin authentication, **not a separate email/password account**.

Create/edit/delete campaigns, publish/unpublish, upload PNG frames, write Bengali/English captions, and copy public links. Frames must be square, 500–6000 px, under 3 MB, and have transparent photo areas. Recommended size: 1080 × 1080. Up to six per campaign.

## Persistent storage

- Campaign metadata: `data/campaigns.json` on the `main` branch.
- Immutable frame assets: `frames/<uuid>.png`.
- Public pages retrieve current campaign metadata directly from GitHub, so admin updates do not require a Vercel rebuild. GitHub/CDN changes may take a short time to propagate.
- Saving uses the current content SHA; simultaneous edits fail safely instead of overwriting another admin's changes. Reload/re-sign in after a conflict.
- Published and draft metadata and artwork are stored in a **public repository**. Draft means hidden from the website, not confidential. Do not store personal or private information in campaign content.
- Deleting a campaign removes its listing/link, not Git history or unreferenced artwork. GitHub retains revision history.
- No visitor photo is sent to a server. No tracking or watermark is added.

## Deploy

Import `Futuristicbd/royel-cement-frame` into Vercel. Framework: **Other**. No build command or environment variables are required; serve the repository root. `vercel.json` configures campaign and admin routes and security headers. Production URL is shareable; turn off deployment protection for public production if enabled in your Vercel account.

The included green/blue demo frames are samples, not supplied final Royal Cement brand artwork. Replace them in Admin with approved transparent PNG frames.

## Local

Run any static server with SPA fallback, e.g. `npx serve .`. Public campaign data uses the GitHub repository. Syntax check: `npm run check`.
