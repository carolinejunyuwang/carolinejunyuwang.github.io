# Caroline Wang — Personal Academic Website

A dependency-free static site in the **refined-serif** style: three hand-written HTML
pages, no generator, no build step. Fonts load from Google Fonts; everything else is
self-contained. Free to host.

## Files
```
website/
├── index.html        ← landing page (edit text/links here)
├── research.html     ← papers + abstracts (currently noindex)
├── hobbies.html      ← photos/videos
├── styles.css        ← shared styles for all three pages
├── robots.txt, sitemap.xml
├── files/
│   ├── cv_caroline.pdf   ← the served CV; copied in from ../cv/, do not hand-edit
│   ├── headshot.jpg
│   └── sunrise*.jpg, drone*.mp4
├── mockups/          ← the two style mockups (reference only; gitignored)
└── README.md
```

## Keeping the CV in sync
The CV's source of truth is `../cv/cv_caroline_wang.tex`. The site links to the **stable path**
`files/cv_caroline.pdf` from the nav on all three pages, so the public link never changes —
note the served filename deliberately differs from the source filename. Updating it is a
deliberate two-step manual process — recompile, then copy:

```bash
cd package/cv
xelatex cv_caroline_wang.tex && xelatex cv_caroline_wang.tex   # twice: longtable + hyperref refs
cp cv_caroline_wang.pdf ../website/files/cv_caroline.pdf
```

The footer date is **not** taken from the compile date — it is set by `\cvdate` in the
preamble, so recompiling never silently changes it. Update it by hand when you re-date the CV.

`xelatex` (not `pdflatex`) is required — the header icons come from `fontawesome5`.
Check the compile log for `Missing character` warnings: the document uses `lmodern`, whose
`ec-lmr10` font has no Unicode em dash (U+2014), so a pasted `—` is **silently dropped**
and jams the surrounding words together. Always write `---` instead.

Then commit and push to redeploy (see below).

Note: the abstracts in the CV and the text on `research.html` are kept in sync by hand —
when you change one, check the other.

## Deploy (GitHub Pages)
This folder **is** the repo root of `carolinejunyuwang/carolinejunyuwang.github.io`.
Pages serves the `main` branch root directly, so a push is the deploy:

```bash
cd package/website
git add -A && git commit -m "..." && git push origin main
```

The live site is `https://carolinejunyuwang.github.io/` and updates within a minute or two.
There is no CI workflow — nothing builds, the files are served as-is.

*(Optional, ~$12/yr)* Add a custom domain: buy it (Cloudflare / Porkbun / Namecheap), add a
`CNAME` file with the domain, set DNS records, and verify the domain in GitHub to prevent
takeover.

## Get found by search / Scholar
- `<title>` and meta description are set for "Caroline Wang — Quantitative Marketing, Kellogg."
- `index.html` carries the Google Search Console verification tag, a canonical link, and
  JSON-LD `Person` schema.
- `research.html` is currently `noindex`; `sitemap.xml` lists only `/` and `/hobbies.html`.
- Keep the **Google Scholar** profile clean and linked.
