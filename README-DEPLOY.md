# SKY TRUST CAPITAL — Netlify Website + Admin CMS

This package upgrades the original STC website source while preserving the supplied company/project images and the five existing project identities. The public layout is newly arranged around the reference website's observed structure: compact sticky navigation, large hero, service cards, project cards, visual gallery, founder/team, About and contact sections. The original reference site's exact CSS/assets were not publicly exposed to inspection, so an exact pixel-for-pixel clone is **not claimed**.

## What's included

- Responsive public website and custom project/page route template.
- `/admin` and `/admin.html` protected dashboard.
- Netlify Function API for login/session, public content, protected content updates and media upload/delete.
- Netlify Blobs site-wide storage (`stc-site-content` and `stc-site-media`). Content is shared across visitors and persists across deploys.
- Five original STC project identities, official logo assets already present in the supplied original ZIP, and the preserved legacy HTML/CSS/JS source under `/legacy/`.
- Editable homepage, navigation, services, projects, pages, opportunities, team, social links, gallery, media settings, design tokens, contact information and SEO metadata.
- Dynamic sitemap, robots.txt, Organization JSON-LD, canonical/Open Graph metadata and security headers.

## Required one-time Netlify setup

**Do not deploy this as a plain drag-and-drop static folder.** Netlify Functions and the Blobs package must be built/deployed. Use Netlify CLI or connect the folder to a Netlify Git deploy. No external database or third-party backend is used.

### 1. Install dependencies and deploy

On a computer with Node.js 22.13+ and npm:

```bash
cd stc-deploy
npm install
npm install --global netlify-cli
netlify login
netlify link
netlify deploy --build --prod --dir=public --functions=netlify/functions
```

When `netlify link` prompts, select the existing STC Netlify site (`skytrustcapital-official`) if this is intended to replace that live site. Review the preview deploy first if the CLI flow offers a draft deploy. Do not select a different site by mistake.

For ongoing updates, use the same linked Netlify project and deploy command, or connect the source repository to Netlify continuous deployment. Ordinary website content edits from `/admin` do **not** require a redeploy.

### 2. Create a strong administrator password hash

Choose your own unique password (minimum 12 characters). Do not put the plain password in this ZIP or in frontend code.

```bash
node scripts/hash-password.mjs "YOUR-OWN-LONG-UNIQUE-PASSWORD"
```

Copy the printed `salt:hash` output. It is a one-way scrypt hash; it is not the original password.

### 3. Set Netlify environment variables

In Netlify: **Project configuration → Environment variables**, add:

| Variable | Value |
|---|---|
| `ADMIN_EMAIL` | `official.skytrustcapital@gmail.com` (or another mailbox you control) |
| `ADMIN_PASSWORD_HASH` | The full `salt:hash` output from step 2 |
| `SESSION_SECRET` | A random secret at least 32 characters long; generate with `openssl rand -base64 48` |

Set the variables for the Production deploy context. Trigger one new production deploy after adding them. Never commit these values into this folder or expose them in browser code.

### 4. First login

Open `https://YOUR-SITE.netlify.app/admin` and sign in with the configured email and the password you chose. The password is checked in the Netlify Function; a signed, HttpOnly, Secure, SameSite=Strict cookie is used for the admin session. Sessions expire after eight hours.

## Live content publishing

The dashboard writes the complete content document to Netlify Blobs. Public pages read the same site-wide content store. This is not browser-local storage. Content is returned using strong consistency reads so the most recently saved data is visible on subsequent public requests. Netlify Blobs is a key/value object store, not a relational database; it is suitable for this site's low-write content and media use case.

If the content store has never been initialized, the public website uses `content-default.json`. The first successful Save & Publish creates the persistent record.

## Upload limits and operational constraints

- Current upload UI/function limit: **4 MB per file**; video files are capped at **3.5 MB** because the browser sends base64 JSON through a Netlify Function request. Compress larger hero videos before uploading. This is an application limit, not a Netlify Blobs object-size limit.
- Uploads are written to Netlify Blobs and served through the site's API function.
- Netlify plan usage, function execution quotas, bandwidth and Blobs storage/operation quotas still apply. Check your current Netlify plan's limits; the ZIP does not promise unlimited free usage.
- Netlify Blobs is site-wide across deploy contexts. Use the production site carefully; do not run destructive tests against production content.
- The contact form opens WhatsApp with a prepared message; it does not store or email submissions.
- No official social profile URLs, investment returns, licences, registration numbers, office addresses, awards or regulatory approvals are fabricated. Investment opportunities start empty and should only be published after documentation/legal review.
- The homepage background video is disabled by default. Upload and enable your own official video in Admin → Media & Logo.

## Admin editing guide

- **Quick Edit:** homepage and section copy.
- **Pages & Records:** create/publish/unpublish/delete custom pages and projects, add team profiles and opportunities, and add verified social profile links.
- **Media & Logo:** upload the official logo and favicon, replace the hero image/video, assign images to team/project/opportunity records, add categorized portfolio images, and remove tracked media.
- **Design:** edit palette, font, logo sizes, section spacing, card radius, button style and header/footer backgrounds. The reference-inspired layout remains intact.
- **Settings & SEO:** company identity, official contact details, canonical URL, SEO metadata and navigation labels/visibility.
- **Advanced Content:** complete JSON-level control of all fields and collections, including detailed project/team/opportunity fields, image order/categories, page templates, social platform links, visibility flags, custom homepage sections and homepage section order. Export/import JSON backups here.

For a custom page, publish it at `/project/your-page-slug`. To show it in the navigation, tick “Add to main navigation” when creating it. Pages not added to navigation remain accessible by direct URL.

## Existing site and reference limitations

- The original ZIP contained an older browser-local Admin Panel; that old login/storage mechanism is retained only as archived source under `/legacy/` and is not used by this live dashboard.
- The supplied legacy project pages are retained under `/legacy/`; their current project content has been represented in the new public project cards and dynamic project routes.
- The reference site was inspectable for its visible structure and text, but its original stylesheets/animation implementation were not retrievable in the inspection environment. The new stylesheet follows the observed hierarchy and layout but exact font metrics, color values, animation timing and responsive breakpoints could not be independently verified against the original source.
- The site cannot be live-deployed or tested against your Netlify account from this workspace because no Netlify account access, site credentials or production environment variables were provided. Do not treat the production deployment, admin authentication against your account, or live Blobs persistence as tested until you complete the steps above.

## Security notes

- Never share `ADMIN_PASSWORD_HASH` or `SESSION_SECRET` publicly.
- Change the administrator password by generating a new hash and replacing the Netlify environment variable, then redeploy.
- Use HTTPS only. Netlify provides HTTPS for its hosted site.
- Keep a downloaded JSON backup after major edits. Media binaries are stored separately in Blobs; JSON backup stores their URLs/IDs but does not contain the binary files.
- Review social URLs and page content before publishing. The API rejects unsafe script/data URL schemes, but administrators remain responsible for the accuracy of their published content.

## Google Search Console

1. Add the deployed domain/property in Google Search Console.
2. Choose the HTML meta-tag verification method and copy the token value (the content value only).
3. In Admin → Settings & SEO, paste it into **Google Search Console verification token**, then Save & Publish.
4. In Search Console, complete verification and submit `https://YOUR-SITE.netlify.app/sitemap.xml`.
5. Monitor indexing reports. Google controls crawling, indexing and ranking; no position or timing is guaranteed.
