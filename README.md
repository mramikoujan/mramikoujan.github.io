# Personal Website — Mohammad Rami Koujan

A single-page static site (HTML + CSS, no build step).

```
personal_website/
├── index.html              # entire page
├── style.css               # all styling
├── README.md               # this file
├── .gitignore
├── images/
│   ├── profile.jpg         # profile photo (drop here; falls back to "MRK" avatar if missing)
│   └── papers/             # publication thumbnails
├── assets/
│   └── cv.pdf              # downloadable CV
└── materials/
    ├── presentations/      # slides (PDF) linked from publications
    ├── recordings/         # talk recordings (MP4)
    └── thumbnails/         # source images/videos used to build paper thumbnails
```

---

## 1. Local preview

```bash
python3 -m http.server 8000
```

Open <http://localhost:8000/> in your browser. Edit `index.html` / `style.css` and refresh.

---

## 2. Updating content

All visible content lives in `index.html`. Edit it directly — no templates, no JS framework.

When the CV is updated, copy the new PDF into `assets/cv.pdf` and keep the bio / experience / education / patents sections in `index.html` consistent with it.

---

## 3. Deploying to GitHub Pages

There are two deploy paths. **Route A is recommended** — it gives you a clean URL like
`https://<username>.github.io/`.

### Route A — User page (recommended)

The repo name **must** be exactly `<username>.github.io` (e.g. `mramikoujan.github.io`).
The site is then served at `https://<username>.github.io/`.

1. Create a new public GitHub repo named `<username>.github.io`.

2. From this folder, initialise and push:

   ```bash
   git init
   git add .
   git commit -m "Initial personal website"
   git branch -M main
   git remote add origin git@github.com:<username>/<username>.github.io.git
   git push -u origin main
   ```

   (Use the HTTPS URL `https://github.com/<username>/<username>.github.io.git` if you don't
   have SSH keys configured.)

3. In the GitHub UI:
   **Settings → Pages → Source: "Deploy from a branch" → Branch: `main`, folder: `/ (root)` → Save.**

4. Wait ~1 minute, then visit `https://<username>.github.io/`.

### Route B — Project page

Use this if you want a different repo name (e.g. `personal_website`). The site is served at
`https://<username>.github.io/<repo-name>/`.

Same `git init` / `git remote add` / `git push` steps as above, with whatever repo name you
choose. Then **Settings → Pages → Branch: `main`, folder: `/ (root)`**.

> Caveat: because the site lives under a subpath, update the absolute URL in `index.html`
> (`og:url`) to include `/<repo-name>/`. Relative paths (`assets/cv.pdf`, `images/...`,
> `style.css`) work as-is.

### Custom domain (optional)

1. Buy a domain.
2. Add a file named `CNAME` to the repo root containing only the bare domain
   (e.g. `ramikoujan.com`). No `https://`, no path.
3. Point the domain's DNS at GitHub's Pages servers — A records to
   `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   (and ideally an `AAAA` record set per
   [GitHub's docs](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site)).
4. In **Settings → Pages**, fill in the custom domain field and tick **Enforce HTTPS** once
   the certificate provisions (usually within a few minutes).

---

## 4. Pre-flight checklist

Open the local preview and confirm:

- [ ] Header renders with photo (or `MRK` initials fallback) and the contact links resolve.
- [ ] Publications section: each row has a thumbnail, bolded own-name, and working
      `[ bibtex ]` toggle.
- [ ] Patents section: monospace patent numbers, reverse-chronological.
- [ ] Selected Projects grid stacks to 1 column on mobile.
- [ ] No console errors in DevTools.

You can validate the HTML at <https://validator.w3.org/nu/> by pasting the source.
