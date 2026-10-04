# ♻️ NIKOLA MD — Pair Site (Standalone)

A standalone, static website for pairing WhatsApp accounts with the **NIKOLA MD** bot. Deploy this anywhere (Vercel, Netlify, GitHub Pages, Cloudflare Pages, or any static host) and it will connect to your bot's API.

## 🚀 Quick deploy

### Option A: Vercel (recommended)
1. Push this folder to a GitHub repo
2. Go to https://vercel.com/new
3. Import the repo → Deploy
4. Visit the deployed URL

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new)

### Option B: Netlify
1. Push this folder to a GitHub repo
2. Go to https://app.netlify.com/start
3. Import the repo → Deploy site

### Option C: GitHub Pages
1. Push this folder to a GitHub repo (e.g. `nikola-pair-site`)
2. Repo → Settings → Pages → Source: `main` branch, `/` root
3. Visit `https://<your-username>.github.io/nikola-pair-site/`

### Option D: Run locally
```bash
npx serve .
# or
python3 -m http.server 8000
```
Then open http://localhost:8000

## ⚙️ Configure the bot server URL

The pair site needs to know where your **NIKOLA MD bot** is running.

1. Open the deployed pair site in your browser
2. Click the **⚙️ Edit** button in the server banner (top right)
3. Enter your bot's URL, e.g. `https://your-bot.herokuapp.com`
4. Click **Save**

The URL is stored in the browser's `localStorage` so users only need to set it once per device.

## 🔌 API endpoints used

The pair site calls these endpoints on your bot:

| Method | Endpoint | Purpose |
|---|---|---|
| POST | `/api/register-session` | Start pairing — returns pairing code |
| POST | `/api/pairing-code` | Poll for updated pairing code |
| POST | `/api/pairing-status` | Check if WhatsApp was successfully linked |

All endpoints expect JSON body: `{ "phone": "2547xxxxxxxx", "password": "master-password" }`

## 🎨 Features

- **3-step flow**: Enter number → Link WhatsApp → Done
- **Live countdown timer** (2 minutes, turns red <30s)
- **Auto-polling** for pairing code updates and status
- **Copy session ID** button on success
- **Server status indicator** — shows if bot is online/offline
- **Configurable bot URL** — point to any NIKOLA MD instance
- **Mobile responsive** — works great on phones
- **No backend needed** — pure static HTML/CSS/JS
- **No build step** — just HTML, deploy as-is

## 🛠️ Customization

### Change default bot URL
Edit the `DEFAULT_SERVER` constant in `index.html`:
```js
const DEFAULT_SERVER = 'https://nikola-md.herokuapp.com';
```

### Change branding
Edit the brand header in `index.html`:
```html
<div class="brand-logo">♻️</div>
<div class="brand-name">NIKOLA MD</div>
<div class="brand-sub">Pair your WhatsApp account</div>
```

### Change colors
Edit CSS variables at the top of `index.html`:
```css
:root {
  --brand:       #7c3aed;  /* purple */
  --brand-light: #8b5cf6;
  --accent:      #06b6d4;  /* cyan */
}
```

## 📦 Files

```
nikola-pair-site/
├── index.html       # The pair site (self-contained)
├── package.json     # For npm serve / Vercel
├── vercel.json      # Vercel config
├── netlify.toml     # Netlify config
├── _config.yml      # GitHub Pages config
└── README.md        # This file
```

## 🔐 Security notes

- The master password is sent over HTTPS to your bot's API — make sure your bot URL is HTTPS
- The password is **not** stored in localStorage (only the bot URL is)
- For production, set up CORS on your bot to only accept requests from your pair site's domain

## 🆘 Troubleshooting

**"Offline" status in banner:**
- Check that your bot is running
- Verify the URL is correct (no trailing slash)
- Make sure your bot's Express server allows CORS (most do by default)

**"Failed to start pairing" error:**
- Verify the master password matches `MASTER_PASSWORD` in your bot's `settings.js`
- Check the bot URL is reachable from your browser

**Pairing code not showing:**
- The bot may have rate-limited pairing requests. Wait 2 minutes and try again.
- Make sure the phone number format is correct (e.g. `254712345678`)

---

♻️ **NIKOLA MD** — Multi-Session WhatsApp Bot
