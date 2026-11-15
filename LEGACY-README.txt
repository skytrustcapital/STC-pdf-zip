SKY TRUST CAPITAL — WEBSITE V2.1 CORPORATE UPGRADE
====================================================

PRESERVED V2 STRUCTURE
- Existing homepage, About page, five project pages, legacy typo redirect, styles, JavaScript and supplied brand assets retained.
- Official project order and spelling:
  1. STC OUTLET
  2. STC ENERGY LAB
  3. STC FOREX VENUES
  4. STC LIVE NETWORK
  5. THE UK SELECT SHOP

V2.1 IMPROVEMENTS INCLUDED
- Premium, visually prominent Founder & Owner profile appears before team members.
- Owner name, designation, introduction, biography, visibility and portrait controls added to the Admin Panel.
- Team profiles display only when named, can be added/removed and have per-profile show/hide controls; additional slots can be added.
- Team cards use coordinated STC accent colors.
- Mission and Vision text are editable in the Admin Panel and render on the homepage.
- Social profile URLs remain editable. Blank profiles remain hidden. Recognizable Simple Icons brand marks are used for TikTok, Instagram, YouTube, Facebook and WhatsApp where URLs are supplied.
- Social icons appear in the homepage social section and footer.
- Homepage introduction video upload/replacement remains available through Media > Homepage introduction video; a remove-video control is added.
- Lightweight STC-palette confetti animation starts on page load, does not intercept clicks, and respects reduced-motion preferences.
- Responsive styling and smooth scrolling refinements added.
- Original local JSON backup/import and IndexedDB media library are retained.

IMPORTANT: LIVE PUBLISHING AND SECURITY LIMITATION
This package is still a static front-end website. The admin's password hash and content are stored in the browser. Uploaded media is stored in that browser's IndexedDB. This is NOT secure owner-only authentication and edits are NOT published to Netlify or synchronized to visitors or other devices.

A secure shared publishing workflow is deliberately NOT faked or enabled in this package. To achieve true owner-only shared editing without a paid backend, configure a server-side Netlify Function that:
1. Authenticates the Owner on the server (never in public JavaScript).
2. Stores a Netlify API token / site credentials only in Netlify environment variables.
3. Validates and sanitizes content/media requests.
4. Creates a new Netlify deploy from the updated site content or writes content to the connected Git repository.
5. Enforces file size/type limits and access controls.

This requires Netlify site ID, a server-side deploy credential, Netlify Functions configuration and a deployment test in the actual Netlify account. Those credentials were not supplied, so no secure live publishing endpoint has been created. Do not put a Netlify token in script.js, HTML, ZIP files or browser storage.

DEPLOY STATIC WEBSITE
1. Extract this ZIP.
2. In Netlify, choose Add new site > Deploy manually (or drag-and-drop deployment).
3. Upload the contents of the folder so index.html is at the published root.
4. Test the homepage and all five project pages.
5. The existing live domain is not modified by this ZIP until you deploy it to the correct Netlify site.

ADMIN PANEL
1. Visit /admin.html.
2. Existing browser-local password setup/sign-in is a convenience gate only, not secure authentication.
3. Company tab: edit company details, mission, vision and Owner profile.
4. Projects tab: edit the five existing project descriptions and images.
5. Team tab: add profiles, edit details, upload portraits, toggle Show profile, or delete a profile; use Add team member for additional slots.
6. Social links tab: enter only confirmed official profile URLs. Blank entries stay hidden.
7. Media tab: choose Homepage introduction video, select a video file and upload. Use Remove homepage video to clear its local reference.
8. Backup tab: export/import JSON content regularly.
9. Media library: download original media separately. JSON backups do not contain binary image/video files.

BACKUP / RESTORE
- Export content JSON from Backup & Restore.
- Download each original uploaded image/video from the Media Library separately.
- Keep both the JSON and media files in a safe location.
- Import JSON to restore text/settings in a browser. Media references only work where the corresponding IndexedDB media records still exist; binary media must be restored separately by a configured workflow.

TESTS PERFORMED ON THIS PACKAGE
- JavaScript syntax checked with Node.js.
- ZIP archive integrity checked.
- All five project page files retained.
- Legacy forex-vanues.html redirect file retained.
- Static HTML parsing / local link checks performed where applicable.

NOT CLAIMED AS TESTED
- Live Netlify deployment or publishing.
- Cross-device synchronization.
- Secure server-side owner authentication.
- Real uploaded media persistence across devices.
- External social icon CDN availability on every network/device.
- Actual Android/iPhone browser rendering in physical devices.
These require deployment and real-device/account testing.

FINANCIAL CONTENT
No guaranteed returns, profit rates, regulatory licences or investment performance claims are added. Investment involves risk, including possible loss of capital. Publish investment offers only after legal review, documentation and appropriate regulatory verification.
