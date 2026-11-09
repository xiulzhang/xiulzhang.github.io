# Personal website

The site is five static pages that share the same header, side rail and styles: `index.html` (About + Contact), `research.html`, `teaching.html`, `fieldnotes.html`, `cv.html` (download box plus the PDF embedded). No build step and no server. Open any page in a browser to preview. Because the header and rail are copied into every page, a change to the rail, nav or CSS has to be made in all five files (search and replace across `*.html`).

## Folder
- `index.html`, `research.html`, `teaching.html`, `fieldnotes.html`, `cv.html`: the pages.
- `photo-180.jpg`, `photo-360.jpg`, `photo-540.jpg`: headshot at 1x/2x/3x for the 180 px slot (head-to-jacket-hem crop of `raw_photos/headshot_202401.jpg`, served via `srcset`). To change the headshot, cut the three sizes from the original with Pillow and bump the `?v=` tag on the `<img>`.
- `img/`: fieldwork photos resized for the web (1400 px long edge, 110 to 360 KB each).
- `raw_photos/`: the original photos. Not published (listed in `.gitignore`).
- `cv.pdf`: **missing**. Compile `../CV.tex` on Overleaf (no LaTeX on this machine), download as `cv.pdf`, and put it here.

## Field notes section
Each story is an `<article class="story">` block inside `<section id="fieldnotes">`: a `.tag` naming the paper, a title, a `.shots` grid of photos, two or three sentences, and a link back to the paper. To add a story, copy a block. Photo width classes: `w12` (full width), `w8` + `w4`, or `w6` + `w6`; add `tall` for portrait photos. To resize a new photo, drop the original into `raw_photos/` and run a copy of the resize step (Pillow, 1400 px long edge, quality 82) or any image tool; keep files under 500 KB.

Papers link to their story with `<a class="fn-link" href="fieldnotes.html#note-...">Field note</a>`.

## Publish on GitHub Pages
The folder is already a git repository with one commit (author Xiuling Zhang, set locally; the machine's global git identity belongs to someone else, so do not drop the local setting).

1. Create a GitHub account if needed (a username close to your name, e.g. `xiulingzhang`).
2. On github.com create a new **public** repository named exactly `<username>.github.io`, with no README, licence, or .gitignore.
3. In a terminal, from this folder:
   ```
   git remote add origin https://github.com/<username>/<username>.github.io.git
   git push -u origin main
   ```
   A browser window opens for GitHub login the first time (Git Credential Manager).
4. Repository Settings > Pages: Source "Deploy from a branch", branch `main`, folder `/ (root)`. Save.
5. After a minute the site is live at `https://<username>.github.io`.

Alternative with the GitHub CLI: `winget install GitHub.cli`, then `gh auth login`, then from this folder `gh repo create <username>.github.io --public --source=. --push`, then enable Pages as in step 4.

To update later: edit, then `git add -A && git commit -m "update" && git push`. GitHub rebuilds within a minute.

## Domain name
Not required. `xiulingzhang.github.io` is professional and free. A custom domain costs about $10-15 per year (Namecheap, Cloudflare, Porkbun). If you buy one: at the registrar add a CNAME record pointing `www` to `<username>.github.io`; in GitHub Pages settings enter the domain and tick "Enforce HTTPS". Do this only after the site works at the github.io address.

## Editing
Each page holds one `<section id="...">` (index.html holds About and Contact). The nav item of the current page carries `aria-current="page"`. On `research.html` papers are grouped by topic: each `<div class="topic">` holds a heading, a one-line `.blurb`, and a `<ul class="pubs">` list (the job market paper sits as a `.jmp` card at the top of Identity Politics). To add a paper, copy one `<li>` block into the right topic and give it a `<span class="status">` badge (Forthcoming, Revise & resubmit, Under review, or Work in progress); to add a topic, copy a whole `.topic` block. Keep the status badges (`<span class="status">`) and the "Last updated" line in the CV box current.
