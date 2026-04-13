# Aura — AI Companion App
## Deployment Guide (Vercel + Netlify)

---

## 📁 Project Structure

```
aura-project/
├── index.html                  ← Main app (ai-companion.html renamed)
├── character.html              ← Character.ai clone (optional)
├── api/
│   └── chat.js                 ← Vercel serverless function
├── netlify/
│   └── functions/
│       └── chat.js             ← Netlify serverless function
├── vercel.json                 ← Vercel config
├── netlify.toml                ← Netlify config
└── README.md
```

---

## 🔑 Step 1 — Get Your Anthropic API Key

1. Go to https://console.anthropic.com
2. Sign in → click **API Keys** in the left sidebar
3. Click **Create Key** → give it a name → copy the key
4. Keep it safe — you'll paste it in the dashboard below

---

## 🚀 Deploy on VERCEL

### Step 1 — Push to GitHub
```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/aura-app.git
git push -u origin main
```

### Step 2 — Connect to Vercel
1. Go to https://vercel.com → Sign up / Log in with GitHub
2. Click **"Add New Project"**
3. Import your GitHub repo
4. Click **Deploy** (default settings are fine)

### Step 3 — Add API Key
1. In your Vercel project → go to **Settings → Environment Variables**
2. Click **Add**:
   - Name: `ANTHROPIC_API_KEY`
   - Value: `sk-ant-your-key-here`
3. Click **Save**
4. Go to **Deployments** → click **Redeploy**

### Step 4 — Update your HTML fetch URL
In `index.html`, change the fetch URL to:
```javascript
const API_URL = '/api/chat';
// Already set if you used the updated HTML files
```

✅ Done! Your Vercel URL will be: `https://aura-app.vercel.app`

---

## 🟢 Deploy on NETLIFY

### Step 1 — Push to GitHub (same as above)

### Step 2 — Connect to Netlify
1. Go to https://netlify.com → Sign up / Log in with GitHub
2. Click **"Add new site" → "Import an existing project"**
3. Choose **GitHub** → select your repo
4. Build settings:
   - Build command: *(leave empty)*
   - Publish directory: `.` (just a dot)
5. Click **Deploy site**

### Step 3 — Add API Key
1. In your Netlify site → go to **Site configuration → Environment variables**
2. Click **Add a variable**:
   - Key: `ANTHROPIC_API_KEY`
   - Value: `sk-ant-your-key-here`
3. Click **Save**
4. Go to **Deploys** → click **Trigger deploy → Deploy site**

### Step 4 — Update your HTML fetch URL
In `index.html`, change the fetch URL to:
```javascript
const API_URL = '/.netlify/functions/chat';
// Already set if you used the updated HTML files
```

✅ Done! Your Netlify URL will be: `https://aura-app.netlify.app`

---

## 🔄 How to Switch Between Vercel & Netlify

In your `index.html`, find this line near the top of the `<script>`:

```javascript
// ── CHANGE THIS LINE DEPENDING ON WHERE YOU DEPLOY ──
const API_URL = '/api/chat';                    // ← Vercel
// const API_URL = '/.netlify/functions/chat'; // ← Netlify (uncomment this one)
```

Just comment/uncomment the correct line before pushing.

---

## 🛡️ Security Notes

- ✅ Your API key is stored as an **environment variable** — never in code
- ✅ GitHub will never see your key
- ✅ Both platforms encrypt environment variables
- ✅ For 2 users, free tier on both platforms is more than enough

---

## 💰 Cost Estimate for 2 Users

- Anthropic free tier: $5 credit on signup
- Claude Sonnet: ~$0.003 per message
- 2 users × 100 messages/day = ~$0.60/day max
- Free credits last weeks/months of casual use

---

## 🆘 Troubleshooting

**"Function not found" error**
→ Make sure `vercel.json` or `netlify.toml` is in the root folder

**CORS error in browser**
→ The proxy functions already handle CORS — make sure you're calling `/api/chat` not the Anthropic URL directly

**API key not working**
→ Double-check there are no spaces before/after the key in the dashboard
→ Redeploy after adding the key

---

Made with ❤️ by Dipesh Kharel
