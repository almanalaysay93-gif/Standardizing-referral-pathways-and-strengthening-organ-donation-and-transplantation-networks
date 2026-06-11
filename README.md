# 4th Transplant MindaNOW — Event Landing Page

Luxury blue-and-gold landing page with built-in registration form for the
**4th Transplant MindaNOW Conference** (July 6–7, 2026, Apo View Hotel, Davao City).

## Files

```
2026-06-11/transplant-mindanow-landing/
├── DOH_logo.png            ← master copies of the three logos
├── spmc_logo.png
├── share_logo.png
└── site/                   ← deploy THIS folder
    ├── index.html          ← the entire website (single file, no build step)
    └── assets/             ← logos the page loads (DOH, SPMC, SHARE)
```

> When you publish, upload the **`site`** folder (it contains `index.html` **and** the
> `assets` folder with the three logos). If you upload only `index.html`, the logos
> will appear broken.

## How the data reaches your Google Sheet

The page does **not** need a server or Apps Script. When a guest clicks
"Confirm my attendance," the page sends their answers directly to your existing
Google Form's submission endpoint:

```
https://docs.google.com/forms/d/e/1FAIpQLSchBHPEyMEauEQ_aBQwquNMqiMlrHB7ZC0ABGCZ7p98ntkiAQ/formResponse
```

Because your Google Form is already linked to a Google Sheet, every submission
from this page appears in that same Sheet automatically — exactly as if the
guest had filled out the Google Form itself.

Field mapping (already wired into the page):

| Page field | Google Form entry ID |
|---|---|
| Full Name | entry.1265900401 |
| Professional Title / Designation | entry.1730735904 |
| Institution / Hospital Affiliation | entry.2123282078 |
| Department | entry.265201630 |
| Active Email Address | entry.1934533468 |
| Mobile Contact Number | entry.1892096209 |
| RSVP Status | entry.1385239179 |
| Dietary Restrictions (+ Other text) | entry.1126767371 |
| Questions for speakers | entry.422836509 |

## Important caveats

- **Do not change the questions in the Google Form.** Editing, reordering, or
  deleting questions changes the entry IDs and silently breaks the page.
  (Changing only the Sheet is fine.)
- **The form must stay open / accepting responses** in Google Forms settings.
- If the form is set to "limit to 1 response" or "require sign-in," guests
  would need a Google account — keep those settings OFF for a public page.
- The page cannot read Google's reply (browser security), so it shows success
  once the request is sent. Do one test registration and confirm the row
  appears in your Sheet before sharing the link.

## How to publish (pick one, all free)

1. **Netlify Drop** — go to https://app.netlify.com/drop and drag the `site`
   folder onto the page. You get a public link in seconds.
2. **GitHub Pages** — upload `index.html` to a repository, enable Pages.
3. **Google Drive won't work** for hosting HTML — use option 1 or 2.

## Local preview

```
python -m http.server 8810 --directory "2026-06-11/transplant-mindanow-landing/site"
```
Then open http://localhost:8810
