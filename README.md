# The Lind Agency — Website Setup Guide

Your site folder contains:

```
lind-agency/
├── index.html      ← the website
├── vercel.json     ← Vercel settings (redirects www → lindagency.com, security headers)
├── sitemap.xml     ← tells Google about your site
├── robots.txt      ← points search engines to the sitemap
└── images/
    └── sterrick.png  ← ADD YOUR PHOTO HERE
```

---

## Step 1 — Add your photo

1. Use a photo of yourself (a transparent-background PNG looks best, like the cut-out on your flyer).
2. Name it exactly **`sterrick.png`** and put it in the `images` folder.
3. If no photo is found, the site shows an "SL" monogram instead, so it never looks broken.

> Tip: remove.bg will make a transparent cut-out for free.

---

## Step 2 — Connect the contact form to Formspree

1. Log in at **formspree.io** with the account tied to **thelindagency@gmail.com**.
2. Click **+ New Form** → name it "Lind Agency Website" → set the email to **thelindagency@gmail.com**.
3. Copy the form endpoint. It looks like: `https://formspree.io/f/xyzabcde`
4. Open `index.html`, search for **`YOUR_FORM_ID`**, and replace it with your ID:
   ```html
   action="https://formspree.io/f/xyzabcde"
   ```
5. In Formspree → your form → **Settings**, add `lindagency.com` under allowed domains (optional but recommended to block spam).
6. After the site is live, submit a test. The first submission may ask you to confirm your email.

---

## Step 3 — Deploy to Vercel

**Option A — Drag and drop (easiest)**
1. Go to **vercel.com** and sign in.
2. Click **Add New → Project**.
3. Choose to deploy without Git / drag your `lind-agency` folder in (or use the Vercel CLI: install Node.js, then run `npx vercel` inside the folder and follow the prompts).
4. Framework Preset: **Other**. Leave build and output settings blank.
5. Click **Deploy**. You'll get a temporary link like `lind-agency.vercel.app` — open it to check everything.

**Option B — GitHub (best for future edits)**
1. Create a new repository on GitHub and upload all files in the folder.
2. In Vercel: **Add New → Project → Import** that repository → **Deploy**.
3. Any time you edit a file on GitHub, Vercel updates the site automatically.

---

## Step 4 — Connect lindagency.com (GoDaddy)

**In Vercel**
1. Open your project → **Settings → Domains**.
2. Add **`lindagency.com`**, then add **`www.lindagency.com`**.
3. Vercel will show the exact DNS records it wants. Keep that page open.

**In GoDaddy**
1. Log in → **My Products** → next to lindagency.com click **DNS** (or **Manage DNS**).
2. Edit/add these records (use the values Vercel shows if they differ):

| Type  | Name | Value                  | TTL      |
|-------|------|------------------------|----------|
| A     | @    | `76.76.21.21`          | 1 hour   |
| CNAME | www  | `cname.vercel-dns.com` | 1 hour   |

3. **Delete** any other `A` record on `@` (GoDaddy often has a "Parked" record) and any existing `www` CNAME pointing elsewhere.
4. Turn off any GoDaddy **Domain Forwarding** for this domain.
5. Do **not** delete MX records — those control email if you ever set it up on this domain.

**Wait & verify**
- DNS usually updates in 10–60 minutes (can take up to 48 hours).
- Back in Vercel → Domains, both entries will show a green **Valid Configuration** check.
- Vercel issues the free SSL certificate (https) automatically.

---

## Step 5 — After launch

- **Google Search Console** (search.google.com/search-console): add `lindagency.com`, verify via the DNS TXT record in GoDaddy, then submit `https://lindagency.com/sitemap.xml`.
- **Google Business Profile**: create a free listing and link the website.
- **When health insurance launches**: in `index.html`, search for "Coming Soon" and update the `#health` section and the footer disclaimer line about health insurance.

---

## Quick edits cheat sheet

| What to change | Search `index.html` for |
|---|---|
| Phone number | `571` |
| Email | `thelindagency@gmail.com` |
| Licensed states | `GA, NC, SC, TX, VA` |
| Colors | `--navy`, `--gold`, `--cream` (top of the `<style>` section) |
| Form endpoint | `formspree.io/f/` |
