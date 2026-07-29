# CCHST Website — static site (HTML/CSS/JS)

Plain static site, no build step, no framework, no Lovable hosting dependency.
Lovable/Figma were only used as design references — this is the real deployable code.

## Structure

```
index.html         Home
about.html          About
programs.html       Programs
admissions.html     Admissions
faculty.html        Faculty
news.html           News & events
gallery.html        Gallery
contact.html        Contact (includes a Netlify Forms contact form)
css/style.css       Shared styles (single stylesheet, all pages)
js/main.js          Scroll-reveal animations, count-up stats, mobile nav toggle
netlify.toml        Security headers (CSP, HSTS, X-Frame-Options, etc.)
assets/             Image files — see below, you need to add these
```

## Before you deploy: add the images

The `assets/` folder is currently empty except for a checklist file. Add these five
image files (same filenames the HTML already points to):

- `logo.jpg`
- `proprietor.jpg`
- `provost.jpg`
- `hod.jpg`
- `staff-yisa.png`

You can pull the originals straight from the old site — visit each URL below,
right-click → Save image as, and drop it into `assets/` with the exact filename:

- https://cchstmakurdi.netlify.app/assets/logo.jpg
- https://cchstmakurdi.netlify.app/assets/proprietor.jpg
- https://cchstmakurdi.netlify.app/assets/provost.jpg
- https://cchstmakurdi.netlify.app/assets/hod.jpg
- https://cchstmakurdi.netlify.app/assets/staff-yisa.png

Delete `assets/PUT_IMAGES_HERE.txt` once that's done.

## Deploy to GitHub → Netlify

1. Create a new empty repository on GitHub (e.g. `cchst-website`).
2. Push this folder's contents to it:
   ```bash
   git init
   git add .
   git commit -m "Initial site"
   git branch -M main
   git remote add origin https://github.com/YOUR-USERNAME/cchst-website.git
   git push -u origin main
   ```
3. In Netlify: **Add new site → Import an existing project → GitHub** → select the repo.
4. Build settings: leave **Build command** empty and set **Publish directory** to `.`
   (this is a static site — nothing to build).
5. Deploy. Netlify will automatically pick up `netlify.toml` and apply the security headers.
6. Once live, go to **Site configuration → Forms** in Netlify to see contact form
   submissions from the Contact page (no backend code needed — Netlify Forms handles it,
   because the form has `data-netlify="true"`).

## What's already handled

- **Bugs fixed:** the old expired admissions deadline copy, dead footer social links,
  and the broken "student portal" link are all resolved.
- **Security:** `netlify.toml` sets CSP, HSTS, X-Frame-Options, X-Content-Type-Options,
  Referrer-Policy, and Permissions-Policy. All external links use `rel="noopener noreferrer"`.
  The contact form has a honeypot field for basic spam protection.
- **Design:** luxury emerald/gold palette, Fraunces + Inter type pairing, scroll-triggered
  reveal animations throughout (respecting `prefers-reduced-motion`).

## What still needs real content

- **News page** currently shows a single placeholder update. Replace with real posts
  as you publish them (simplest option: duplicate the `.notice-panel` block per story).
- **Gallery page** only has the four staff photos and the crest. Add real campus/event
  photos to `assets/` and drop new `<div class="gallery-item"><img ...></div>` blocks
  into `gallery.html`.
- **Faculty page** lists the four people known from the current site. Add more staff
  the same way as the existing `.team-card` blocks.
- **Admissions requirements list** on `admissions.html` is a reasonable standard list
  (SSCE result, birth certificate, passport photos, ID) — confirm it matches your
  actual requirements before publishing.
