# juliusjackson.com — personal site

A single-page, fully static site (one `index.html` + an `assets/` folder). No build step, no framework, nothing to compile. It works the moment it's hosted.

```
site/
├── index.html              ← the whole site (HTML + CSS + JS inline)
├── assets/
│   ├── headshot-suit.png    (hero photo)
│   ├── headshot-hat.png     (about photo)
│   ├── book-is-that-fair.png
│   ├── book-love-life.png
│   ├── headshot-casual.png  (spare — not currently used)
│   └── Julius_Jackson_Resume.docx  ← the "Download Résumé" button serves this
└── README.md
```

---

## ⚠️ First: revoke that GitHub token

You pasted a GitHub personal access token into the chat. Treat it as compromised. Go to **GitHub → Settings → Developer settings → Personal access tokens** and delete it now. The steps below let you push without ever sharing a token.

---

## Deploy — pick the easiest path

### Option A — Netlify drag-and-drop (≈60 seconds, no GitHub needed)
1. Go to **https://app.netlify.com/drop**
2. Drag the **`site`** folder onto the page.
3. It's live at a `*.netlify.app` URL instantly. Done.

### Option B — Push to your GitHub repo, then connect Netlify *or* Vercel
Run these in a terminal from inside the `site` folder (replace nothing — it uses your existing repo):

```bash
cd site
git init
git add .
git commit -m "Launch juliusjackson.com"
git branch -M main
git remote add origin https://github.com/villa9e/juliusjackson.git
git push -u origin main
```
When it asks you to authenticate, log in through the browser prompt (or use a **fresh** token you create after revoking the old one).

Then in **Netlify** or **Vercel**:
- **Netlify:** New site → Import from Git → pick the repo → **Build command: none**, **Publish directory: `/`** (or `site` if you push the parent folder). Deploy.
- **Vercel:** Add New → Project → import the repo → **Framework Preset: Other**, leave build empty, **Output Directory: `./`**. Deploy.

### Connect the custom domain (juliusjackson.com)
After deploying, open **Domain settings** in Netlify/Vercel, add `juliusjackson.com`, and point your domain registrar's DNS at the records they show you (an `A`/`ALIAS` record for the apex and a `CNAME` for `www`). HTTPS is automatic and free.

---

## Editing things

- **Logos in the scrolling band** are clean text "wordmark" chips (works everywhere, no copyright headaches, and looks more cohesive than mismatched PNGs). To swap any chip for a real logo image, drop the file in `assets/logos/` and edit the `makeChip` function near the bottom of `index.html` to return an `<img>` instead of text. The company list lives in the `companies` array right above it — add/remove names there.
- **Experience** entries live in the `roles` array in `index.html`. Roles flagged `tech:true` get the filled gold timeline dot.
- **Résumé download** points to `assets/Julius_Jackson_Resume.docx`. Replace that file (keep the name) to update the download. If you'd rather serve a PDF, drop a PDF in `assets/` and change the two `href="assets/Julius_Jackson_Resume.docx"` links.
- **Colors/fonts** are CSS variables at the very top of the `<style>` block (`--gold`, `--ink`, etc.).

## Note on dates
The work history is sequenced as a continuous, non-overlapping arc from 2008 to present (per your request to spread it across 18 years). Double-check each date range matches how you want to represent your timeline before sharing widely.
