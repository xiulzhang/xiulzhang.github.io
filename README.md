# Personal website

The site is five static pages with one shared stylesheet (`style.css`): `index.html` (About), `research.html`, `teaching.html`, `fieldwork.html` (Fieldwork Gallery), `cv.html` (download box plus the PDF embedded). Every page has the same shell: a full-width banner photo (`img/hero.jpg`, a crop of `raw_photos/new.jpg`, the "The City Is Yours" Lagos photo), a left column (name, headshot, affiliation, email, CV link) and a right column with the tab navigation and the page content. No build step and no server. Open any page in a browser to preview. Styles live only in `style.css`; the banner, left column and tabs are copied into every page, so a change to them has to be made in all five files. `fieldnotes.html` is only a redirect to `fieldwork.html` for old links.

## Folder
- `index.html`, `research.html`, `teaching.html`, `fieldwork.html`, `cv.html`: the pages. `style.css`: all styles.
- `photo-180.jpg`, `photo-360.jpg`, `photo-540.jpg`: headshot at 1x/2x/3x for the 180 px slot (head-to-jacket-hem crop of `raw_photos/headshot_202401.jpg`, served via `srcset`). To change the headshot, cut the three sizes from the original with Pillow and bump the `?v=` tag on the `<img>`.
- `img/`: fieldwork photos resized for the web (1400 px long edge, 110 to 360 KB each).
- `font/name-zh.woff2`: Source Han Serif SC cut down to the three characters 张琇玲 (2.7 KB). The full font `font/SourceHanSerifSC-VF.otf` (55 MB) stays local and is not published (listed in `.gitignore`). If the Chinese name changes, rebuild with `python -m fontTools.subset font/SourceHanSerifSC-VF.otf --text="..." --flavor=woff2 --output-file=font/name-zh.woff2`.
- `raw_photos/`: the original photos. Not published (listed in `.gitignore`).
- `cv.pdf`: **missing**. Compile `../CV.tex` on Overleaf (no LaTeX on this machine), download as `cv.pdf`, and put it here.

## Fieldwork Gallery
`fieldwork.html` is a grid of photos, each a `<figure>` with a one-line `<figcaption>`, inside `<div class="shots">`. To add a photo, copy a `<figure>`. Width classes: `w12` (full width) or `w6` + `w6` (two side by side); add `wide` for a 16:9 crop or `tall` for portrait photos. To resize a new photo, drop the original into `raw_photos/` and resize with Pillow (1400 px long edge, quality 82) or any image tool; keep files under 500 KB.

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
The tab of the current page carries `aria-current="page"`. On `research.html` papers are grouped by topic: each `<div class="topic">` holds an `<h2>` and a list of `<article class="paper">` blocks (title, authors, a `<span class="status">` badge, an optional `Manuscript` link, and the abstract inside `<details>`, which opens on click). The job market paper is an ordinary block with the badge "Job Market Paper". To add a paper, copy one `<article class="paper">` block into the right topic; to add a topic, copy a whole `.topic` block. To change the banner, crop a wide band (about 2.6:1) from a photo, save it as `img/hero.jpg`, and bump `?v=` on the `<img>` in each page. Keep the status badges and the "Last updated" line in the CV box current.
