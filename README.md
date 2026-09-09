# David Lloyd Design — Portfolio Site Export

This is a complete, self-contained export of the David Lloyd Design portfolio site — the same site currently live as a Claude Artifact, exported to real files for hosting anywhere (Hostinger, Netlify, GitHub Pages, any static web host).

## What's in this package

```
index.html        The entire site — structure, styling (CSS), and behavior (JavaScript) in one file
images/            95 JPG/PNG files — project photography, spreads, logos, portraits
video/             1 MP4 file — a looping background clip kept in the codebase (not currently used on the live homepage)
README.md          This file
```

There is no build step, no framework, and no dependencies. `index.html` is plain HTML5 with inline CSS (in a `<style>` block) and inline vanilla JavaScript (in a `<script>` block, no React or other framework) that renders the whole site client-side from a single JavaScript state object (`DEFAULT_STATE`) containing all the site's copy — headings, project descriptions, testimonials, contact details, etc.

## How the site works

- All page content (site copy, navigation, the list of projects, testimonials) lives in one JavaScript object called `DEFAULT_STATE` near the top of the inline `<script>` in `index.html`.
- All images and video are referenced by relative path (e.g. `images/wbh_cover.jpg`, `images/portrait_battersea.jpg`) — nothing is embedded as base64, so the `images/` and `video/` folders must stay alongside `index.html` with their folder structure intact.
- The homepage hero is an animated crossfade slideshow (`heroVisual.slideshow` in `DEFAULT_STATE`) that cycles through a portrait and a few pieces from the Artworks section, each with a slow zoom. It's pure CSS animation, no JavaScript timers.
- Fonts: the site uses system fonts only (no external font files or Google Fonts) — see the `font-family` rules near the top of the `<style>` block if you want to swap in a custom typeface.
- Navigation between pages (Home, Work, About, Services, Contact, individual project pages) is handled client-side via the URL hash (e.g. `#project=p_wbh`), so the site works as a single HTML file with no server-side routing required.
- The left-hand sidebar menu blurs unfocused links on hover (see `.side-nav:hover .side-link:not(:hover)` in the CSS) for a soft focus effect.
- An "Edit site" mode is built into the page itself (bottom-left button) — it lets you click into text on the page and edit copy directly in the browser, then export the updated state. This is a convenience for quick content tweaks; for structural changes (new projects, layout changes) editing the `DEFAULT_STATE` object or the HTML/CSS directly is more reliable.

## How to host this

### Option A: Static host with drag-and-drop or FTP (Hostinger, etc.)
1. Upload `index.html`, the `images/` folder, and the `video/` folder to your site's root (or a subfolder) via File Manager or FTP, preserving the folder structure exactly as it is here.
2. Point your domain/subdomain at that folder. No further configuration needed.

### Option B: Git-based auto-deploy (GitHub + Netlify, Vercel, etc.)
1. Initialize a git repo in this folder: `git init`
2. `git add .`
3. `git commit -m "Initial commit"`
4. Add your remote and push: `git remote add origin <your-repo-url>`, `git branch -M main`, `git push -u origin main`
5. In Netlify (or similar), choose "Import from Git," select the repo, and deploy with default settings — no build command needed since this is a static site (leave "build command" blank and set the publish directory to the repo root).

### Option C: GitHub Pages
1. Push this folder to a GitHub repo as above.
2. In the repo's Settings → Pages, set the source to the `main` branch, root folder.

## Notes

- Total package size is roughly 11MB, almost entirely the images folder — well within any static host's limits.
- If you add new projects or images going forward, keep new images in `images/` and reference them by the same relative-path pattern already used in `DEFAULT_STATE`.
- The `video/homepage_loop.mp4` file and its reference in the code are left in place but unused by default (the homepage currently uses the image slideshow instead) — safe to delete both if you want to trim the package further.
