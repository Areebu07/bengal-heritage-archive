# Bengal Heritage Archive website

A static multi-page site (no build step): `index.html` (home), `catalog.html`, `reading-room.html`, `explore.html` (map, quiz, timeline), `guide.html` (records guide, glossary), `papers.html`, `about.html` (about, standards, privacy) and `contact.html` (FAQ, contact). Shared styles are in `assets/site.css` and scripts in `assets/site.js`; the book list, hosted-file map and district data are at the top of `site.js`. The language menu sets Google's `googtrans` cookie and reloads; choosing English clears it plus the PDFs in `books/` (about 945 MB in 67 files, each under 25 MB so they fit Cloudflare Pages' 25 MiB per-file cap and GitHub's 100 MB limit). `books/catalog/` holds the hosted copies of the Internet Archive catalog books; long books are split into `-partN.pdf` files. A repo this size is near GitHub's recommended 1 GB; Cloudflare Pages handles it, but keep the repo public and avoid re-committing PDFs. Fonts load from Google Fonts; everything else is inline.

## Credibility pieces
`about.html` holds the founder note, the method (how each entry is checked), the corrections log and the privacy note. Add a dated line to the corrections log (`#corrections`) whenever a card is fixed. `sitemap.xml` and the canonical and social tags use `https://waymark.areebuzzaman.com/`; update them if the address changes. `404.html` is served for unknown paths (`not_found_handling` in `wrangler.jsonc`).

## Before going live
- Contact email is archive@areebuzzaman.com (set).
- Fill the remaining placeholder: the founder's personal note under "How it started" in `about.html`.
- Confirm the working name "Bengal Heritage Archive" isn't already taken (search the name, IRS Tax Exempt Organization Search, Maryland SDAT business search).
- Keep the footer wording ("independent, volunteer-run project ... not a registered nonprofit") until the organization is incorporated and IRS-recognized.
- Family papers stay "Closed" and unnamed until the family signs off. No photos of living people.

## Address
Best: a free subdomain of an existing domain, such as `waymark.areebuzzaman.com`, pointed at the Cloudflare project (Custom domains). Otherwise use the free `<project>.pages.dev` or `<project>.workers.dev` address.

## Language and theme
The language menu drives the Google Translate widget, with its banner hidden and the menu's own language names kept untranslated. The light/dark button remembers the choice in the browser. Both are in `index.html`.

## Host it free on Cloudflare Pages (recommended)
1. Put `index.html`, `robots.txt` and the `books/` folder in a GitHub repo (for example `bengal-heritage-archive`).
2. Sign in at dash.cloudflare.com, go to Workers & Pages, Create, Pages, Connect to Git.
3. Pick the repo. Framework preset: None. Build command: leave empty. Output directory: `/`.
4. Deploy. The site is live at `<project-name>.pages.dev`. Each push to `main` redeploys.

## Or GitHub Pages
1. In the repo, Settings, Pages.
2. Source: Deploy from a branch, branch `main`, folder `/ (root)`. Save.
3. The site appears at `https://<username>.github.io/<repo>/` in a minute or two. (Free GitHub Pages needs a public repo.)

## Editing the catalog
The books are the `BOOKS` list near the bottom of `index.html`. Each row is
`[theme, title, author, year, why it matters, link, starred (1 or 0), context note]`.
Hosted PDFs for a book are listed in the `FILES` map, keyed by the Internet Archive id at the end of its link.
Themes: GAZ (places and gazetteers), HIS (history), MAP (maps and census), SOC (people and society), LIT (literature).
Call numbers are generated from theme, year and order.

## Adding a PDF to the Reading room
Copy the file into `books/` and add a row to the `READING` list in `index.html`. Only add works published in 1930 or earlier. Keep each file under 15 MB, or split it into parts. Family papers and anything newer stay out until written permission is on file.
