# Siggy Proxy — Deploy Guide

## What this is
A tiny Vercel serverless function that acts as a CORS-safe proxy between
your GitHub Pages frontend and the Anthropic API.

---

## Step 1 — Create a new GitHub repo for the proxy

Name it something like `siggy-proxy`. Push these files to it:
```
siggy-proxy/
├── api/
│   └── chat.js
├── package.json
└── vercel.json
```

---

## Step 2 — Deploy to Vercel (free)

1. Go to https://vercel.com and sign in with GitHub
2. Click **Add New → Project**
3. Import your `siggy-proxy` repo
4. Click **Deploy** (no build settings needed)

---

## Step 3 — Add your Anthropic API key

1. In Vercel dashboard → your project → **Settings → Environment Variables**
2. Add:
   - **Name:** `ANTHROPIC_API_KEY`
   - **Value:** your key from https://console.anthropic.com
3. Click **Save** then **Redeploy** (Deployments tab → ••• → Redeploy)

---

## Step 4 — Update your frontend

In `index.html`, find this line near the top of the `<script>` block:

```js
const PROXY_URL = 'https://YOUR-PROJECT-NAME.vercel.app/api/chat';
```

Replace `YOUR-PROJECT-NAME` with your actual Vercel project name.
You can find the full URL on your Vercel project dashboard.

Example:
```js
const PROXY_URL = 'https://siggy-proxy.vercel.app/api/chat';
```

Then push the updated `index.html` to your `RitualistSiggy.github.io` repo.

---

## Done!

Your site at `https://ritualistsiggy.github.io` will now talk to Vercel,
which securely forwards requests to Anthropic with your API key.
The API key is never exposed to the browser. 🔥
