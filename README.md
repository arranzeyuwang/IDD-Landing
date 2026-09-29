# Accessible Data Storytelling — Study Landing Page

A single-page, fully static recruitment site for the IDD Accessible Data Storytelling study.
No build step, no dependencies — just HTML and CSS.

```
idd-storytelling-landing/
├── index.html    ← the page
├── styles.css    ← all styling
├── vercel.json   ← optional static-site config
└── README.md
```

---

## 1. Before you publish — fill in the two placeholders

Open `index.html` and search for `example.org`. There are **three** spots to update:

| # | What it is | Where | Current value |
|---|-----------|-------|---------------|
| 1 | **Example study link** (hero button) | `id="top"` hero → "See an example study" | `https://example.org/example-study` |
| 2 | **Example study link** (banner button) | `id="how"` section → "View the example study" | `https://example.org/example-study` |
| 3 | **Sign-up form link** | `id="signup"` section → "Go to the sign-up form" | `https://example.org/sign-up-form` |

Each is marked with an HTML comment, e.g.:

```html
<!-- EXAMPLE STUDY LINK — replace the href below with the real example study URL -->
<a class="btn btn-secondary" href="https://example.org/example-study" ...>
```

Replace `https://example.org/example-study` with your real example-study URL and
`https://example.org/sign-up-form` with your Qualtrics / Google Form URL. That's it.

**Also worth a quick check:** the contact name and email (`Maggie Xu`, `maggiexu@umd.edu`)
appear in the hero-adjacent contact section, the footer, and several `mailto:` links.
The IRB block (`IRB #24-1796`, `IRB_subjects@unc.edu`, `(919) 966-3113`) is in the footer.

---

## 2. Preview locally

Just double-click `index.html`, or run a local server:

```bash
cd idd-storytelling-landing
python3 -m http.server 8000
# then open http://localhost:8000
```

---

## 3. Deploy free on Vercel

### Option A — Drag & drop (easiest, no tools installed)

1. Go to **https://vercel.com/signup** and create a free account (GitHub/Google/email).
2. Go to **https://vercel.com/new**.
3. Drag the whole `idd-storytelling-landing` folder onto the upload area.
4. Vercel detects a static site automatically — leave every build setting as-is.
5. Click **Deploy**. You get a live URL in about 20 seconds, e.g.
   `https://idd-storytelling-landing.vercel.app`.

> Note: drag-and-drop deployments don't auto-update. To change the page later,
> edit the files and repeat, or use Option B/C.

### Option B — Vercel CLI (best for quick updates)

```bash
# 1. Install the CLI (needs Node.js — you already have v22)
npm install -g vercel

# 2. From inside the project folder
cd idd-storytelling-landing
vercel login          # opens your browser to authenticate
vercel                # deploys a PREVIEW url — safe to test
vercel --prod         # promotes it to your PRODUCTION url
```

Every future update is just: edit the files → run `vercel --prod`.

### Option C — GitHub + Vercel (auto-deploy on every change)

1. Create a new repository on GitHub and push this folder:

   ```bash
   cd idd-storytelling-landing
   git init
   git add .
   git commit -m "Add study landing page"
   git branch -M main
   git remote add origin https://github.com/YOUR-USERNAME/idd-storytelling-landing.git
   git push -u origin main
   ```

2. In Vercel: **Add New → Project → Import** the repository.
3. Framework Preset: **Other**. Build Command: *(leave empty)*.
   Output Directory: *(leave empty — Vercel serves the repo root)*.
4. Click **Deploy**.

From then on, every `git push` to `main` redeploys automatically, and every pull
request gets its own preview URL you can share with the research team before going live.

---

## 4. What you get on the free tier

- **Free HTTPS** on a `*.vercel.app` subdomain
- **Global CDN** — fast from anywhere, including on slow connections
- **Custom domain** support (e.g. `datastorystudy.org`) at no extra cost —
  add it under Project → Settings → Domains, then point your registrar's DNS
  (`A` record to `76.76.21.21`, or a `CNAME` to `cname.vercel-dns.com`)
- Generous bandwidth for a recruitment page; no credit card required

### Alternatives if you'd rather not use Vercel

| Platform | How | Notes |
|---|---|---|
| **Netlify Drop** | Drag the folder onto https://app.netlify.com/drop | Zero-config, instant URL |
| **Cloudflare Pages** | Connect a GitHub repo | Very fast, unlimited bandwidth |
| **GitHub Pages** | Repo → Settings → Pages → deploy from `main` / root | Free, but slower to update |

---

## 5. Accessibility notes (built in)

Because the study is about accessibility, the page itself follows WCAG 2.1 AA:

- Semantic landmarks (`header` / `nav` / `main` / `footer`) and a correct heading order
- A visible **"Skip to main content"** link for keyboard and screen-reader users
- Text contrast at or above 4.5:1 throughout; links at ~7.5:1
- A **visible focus ring** on every interactive element (never removed)
- Base font size scales from 17px to 19px; all sizes in `rem` so browser zoom works
- Buttons carry a small "(opens in a new tab)" note so the new-tab behaviour is announced
- Full `prefers-reduced-motion` and `prefers-contrast: more` support
- The hero illustration has a `<title>` + `<desc>` for screen readers
- A **print stylesheet** — printing the page produces a clean paper flyer with URLs shown
- Works with JavaScript disabled (the only script is the footer year)

If you add content later, keep the heading order intact and give every image an `alt` text.

---

## 6. Content source

All copy is taken from the study flyer: eligibility criteria (18–60, lived IDD experience,
legally responsible for self, computer + reliable internet), the one-hour Zoom session,
the $50 gift card, the assistive-technology note, and the IRB statement
(UNC-Chapel Hill IRB #24-1796).
