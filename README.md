# louisebernard.org — personal site

Four-page static site. Drop it on any static host and you're done.

## Files

```
index.html       Home (intro + bio paragraphs)
research.html    Working papers
cv.html          Full CV inline + PDF download button
contact.html     Direct contact + form
assets/
  style.css      All styling (Hauser-inspired, warm cream + navy)
  cv.pdf         Your CV (already copied in)
  portrait.jpg   Headshot — NOT INCLUDED, see below
```

## Before going live — small fixes

### 1. Add your portrait
Drop a JPG named `portrait.jpg` into `assets/`. Aspect ratio 4:5 looks best (e.g. 800×1000 px). The Slack avatar URL you sent is auth-protected so I couldn't pull it automatically — the home page currently shows a placeholder until you add the file.

### 2. Activate the contact form
The form on `contact.html` is wired for Formspree (5-min setup, free tier handles 50 messages/month):
1. Sign up at https://formspree.io with your gmail
2. Create a new form, copy the form ID
3. In `contact.html`, replace `YOUR_FORM_ID` with your actual ID

If you'd rather skip the form, just delete the right column on `contact.html` — the email, Scholar, and LinkedIn links on the left side already do the job.

### 3. Optional: add ETAP start year
On `cv.html` under Affiliations I've put `2025 —` as the start date. Adjust if needed.

## Hosting (replacing the Google Sites page)

Google Sites won't accept raw HTML, so the path is:

**Option A — GitHub Pages (free, easiest)**
1. Create a new GitHub repo, e.g. `louisebernard.github.io`
2. Upload all files in this folder to the repo root
3. Settings → Pages → Source: `main` branch
4. Live at `https://louisebernard.github.io` within a minute
5. To use a custom domain (e.g. `louisebernard.org`), add a `CNAME` file with the domain and update DNS

**Option B — Netlify (free, drag-and-drop)**
1. Sign up at netlify.com
2. Drag the entire site folder onto the dashboard
3. Done — instant URL like `louisebernard.netlify.app`
4. Add a custom domain in Netlify's UI if desired

**Option C — Cloudflare Pages**
Same idea, free tier, very fast. Slightly more setup than Netlify but better long-term if you ever want server-side bits.

Once your new site is live, edit your old Google Sites page and either redirect to the new URL or replace the content with a single line linking to the new site.

## Customisation notes

- Colours, fonts, and spacing all live in `assets/style.css` under `:root`. The two key variables are `--paper` (background) and `--accent` (navy). Change them and the whole site retones.
- Body font is Cormorant Garamond, UI font is Inter — both loaded from Google Fonts.
- The home page bio is in `index.html` between the four `<p>` tags inside `.prose`. Edit there.
- Add new papers to `research.html` by copying any `<article class="paper">` block.

## Things I left out (tell me if you want them back)

- Outreach / writing page — Hauser has one, but you didn't list any pieces and I didn't want to invent.
- Press / media mentions section.
- Twitter/X, ORCID, GitHub icons — not in your data, easy to add.
- Newsletter signup, blog, RSS — overkill for a four-page personal site, can add later.
