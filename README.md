# Synthara Forge — Website

A dark-themed, single-page marketing site for Synthara Forge with a working contact form.

**Stack:** Pure HTML + CSS + vanilla JS. No build step. No dependencies. Drop it on GitHub Pages and you're live.

---

## Quick Preview

Open `index.html` in any browser to preview locally — that's the whole site.

---

## Publishing to GitHub Pages (Step-by-Step)

### Option A: User/Org Site at `https://<username>.github.io`

Use this if you don't already have a `<username>.github.io` repo. The site will live at the root domain.

**1. Create the repo on GitHub**
- Go to https://github.com/new
- Repository name: `<your-username>.github.io` (e.g. if your username is `janedoe`, name it `janedoe.github.io`)
- Set to **Public**
- Do **not** initialize with a README (we have our own files)
- Click **Create repository**

**2. Push the files**

From the `syntharaforge/` folder on your machine, run:

```bash
git init
git add .
git commit -m "Initial site"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-username>.github.io.git
git push -u origin main
```

**3. Enable GitHub Pages**
- In the repo, go to **Settings → Pages**
- Under **Build and deployment → Source**, select **Deploy from a branch**
- Branch: `main`, folder: `/ (root)`
- Click **Save**

**4. Wait ~1–2 minutes**, then visit `https://<your-username>.github.io`. The site is live.

---

### Option B: Project Site at `https://<username>.github.io/syntharaforge`

Use this if you want it as a sub-path (e.g. you already have a user site).

**1. Create the repo**
- Repository name: `syntharaforge` (or anything you like)
- Public, no auto-README

**2. Push the files** (same git commands as Option A, but with the new repo URL)

**3. Enable Pages** the same way (Settings → Pages → Deploy from branch → main → root)

**4. Site lives at** `https://<your-username>.github.io/syntharaforge`

---

### Option C: Custom Domain (e.g. `syntharaforge.com`)

Once Option A or B is working, add your own domain:

**1. Buy a domain** from Namecheap, Cloudflare Registrar, Porkbun, etc.

**2. In your repo's Settings → Pages → Custom domain**, enter `syntharaforge.com` and save.

**3. At your DNS provider**, add these records:

For an apex domain (`syntharaforge.com`):
```
A    @    185.199.108.153
A    @    185.199.109.153
A    @    185.199.110.153
A    @    185.199.111.153
```

For a www subdomain (`www.syntharaforge.com`):
```
CNAME    www    <your-username>.github.io
```

**4. Wait for DNS to propagate** (minutes to a few hours), then check **Enforce HTTPS** in the Pages settings.

---

## Wiring Up the Contact Form

The form is built but needs an endpoint to actually deliver submissions to your inbox. GitHub Pages is static — it can't process form data on its own — so you use a free third-party service.

### Recommended: Formspree (free tier, 2-minute setup)

**1. Sign up at https://formspree.io** (free, no credit card)

**2. Create a new form**
- Click **+ New Form**
- Form name: `Synthara Forge Dataset Requests`
- Send to: your email
- Click **Create Form**

**3. Copy your form endpoint** — it looks like `https://formspree.io/f/xyzabcde`

**4. Paste it into `index.html`**

Find this line in `index.html` (around line 700, in the `<form>` tag):

```html
<form id="contactForm" action="https://formspree.io/f/YOUR_FORMSPREE_ID" method="POST">
```

Replace `YOUR_FORMSPREE_ID` with the ID from your endpoint:

```html
<form id="contactForm" action="https://formspree.io/f/xyzabcde" method="POST">
```

**5. Commit and push:**

```bash
git add index.html
git commit -m "Wire up Formspree endpoint"
git push
```

**6. Test the form** on your live site. The first submission will trigger a Formspree confirmation email to verify the recipient address.

### Alternatives to Formspree

If you'd rather use something else:

- **Web3Forms** (https://web3forms.com) — also free, similar setup
- **Getform** (https://getform.io) — free tier, 50 submissions/month
- **Basin** (https://usebasin.com) — free tier, 100 submissions/month
- **Netlify Forms** — if you migrate hosting to Netlify, forms are built-in (free up to 100/month)

All work the same way: sign up, get an endpoint URL, paste into the `<form action="...">` attribute.

### Until you configure an endpoint

The form is in **demo mode** by default — submitting it will show the success state but won't actually send anything. This is intentional so you can preview the UI before wiring up the backend.

---

## Updating the Site

After the initial push, edit `index.html` locally and run:

```bash
git add index.html
git commit -m "Describe what changed"
git push
```

GitHub Pages will redeploy automatically within 1–2 minutes.

---

## File Structure

```
syntharaforge/
├── index.html      # Entire site — HTML, CSS, JS all inline
└── README.md       # This file
```

That's it. One file. No build step, no `node_modules`, no framework.

---

## What to Customize Before Going Live

Before sharing the URL with prospects, edit `index.html` and update:

1. **Email address** — search for `hello@syntharaforge.com` (appears in the contact section and form disclaimer) and replace with your real address.
2. **Footer location** — change `FORGED IN CALIFORNIA · USA` to wherever you're based.
3. **Founding year** — `Est. 2026` in the hero eyebrow if needed.
4. **Stats** — the four numbers in the stats bar (Domains, Sample Turnaround, Verification, Methodology) are reasonable defaults; adjust to taste.
5. **Formspree endpoint** — as covered above.
6. **Favicon** (optional) — add a `<link rel="icon" ...>` tag in `<head>` if you want a tab icon. Use https://realfavicongenerator.net for a quick one.

---

## Browser Support

Works in all modern browsers (Chrome, Firefox, Safari, Edge — last 2 versions). No IE support; the design uses CSS variables, grid, backdrop-filter, and modern font loading.

---

## License

Site code is yours to use however you want for Synthara Forge. Fonts are loaded from Google Fonts under their respective open licenses.
