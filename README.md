# Caroline Wang — Personal Academic Website

A single-file, dependency-free site (`index.html`) in the **refined-serif** style.
Fonts load from Google Fonts; everything else is self-contained. Free to host.

## Files
```
website/
├── index.html        ← the site (edit text/links here)
├── files/
│   └── cv.pdf         ← stable link target; auto-generated, do not hand-edit
├── update-cv.sh       ← recompiles ../cv/cv_caroline.tex → files/cv.pdf
├── mockups/           ← the two style mockups (reference only; safe to delete)
└── README.md
```

## Keeping the CV in sync
Your CV's source of truth stays at `../cv/cv_caroline.tex`. The website links to the
**stable path** `files/cv.pdf`, so the link on the site never changes. After editing the CV:

```bash
cd package/website
./update-cv.sh        # recompiles the .tex and copies the fresh PDF to files/cv.pdf
```

Then redeploy (see below). The "CV" nav link and the "Curriculum Vitae" button both point to `files/cv.pdf`.

## To finish before going live
- [ ] **Headshot.** Drop a photo at `files/headshot.jpg`, then in `index.html` replace
      `<div class="photo">Your<br>headshot</div>` with
      `<img class="photo" src="files/headshot.jpg" alt="Caroline Wang">`.
- [ ] **Real links.** Fill in the `href="#"` placeholders: JMP PDF/slides, working-paper PDFs,
      the HBR article URL, your Google Scholar profile, and LinkedIn.
- [ ] **Confirm JMP authorship** ("with Anocha Aribarg" vs. solo) so the site, CV, and
      research statement agree.

## Deploy for free (GitHub Pages)
1. Create a public repo named `carolinewang.github.io` (use your GitHub username).
2. Put the contents of this `website/` folder at the repo root (so `index.html` is at the top).
3. Push. In **Settings → Pages**, set the source to the `main` branch, root. Your site is live at
   `https://<username>.github.io/` within a minute or two.
4. *(Optional, ~$12/yr)* Add a custom domain (e.g. `carolinejwang.com`): buy it (Cloudflare /
   Porkbun / Namecheap), add a `CNAME` file with the domain, set DNS records, and verify the
   domain in GitHub to prevent takeover.

Alternatives that are equally free: **Netlify** (drag-and-drop the folder) or **Quarto Pub**.

## Get found by search / Scholar
- The `<title>` and meta description are already set for "Caroline Wang — Quantitative Marketing, Kellogg."
- Create/clean your **Google Scholar** profile and link it.
- After deploying, submit the URL to **Google Search Console** to index in days, not months.
