# BlueRoots Foundation — Deploy Guide

## Folder Structure
```
blueroots-deploy/
├── index.html          ← the static site
├── videos/             ← 6 video files
└── api/
    └── chat.js         ← Vercel serverless function (AI agents)
```

## One-Time Setup

### 1. Get an Anthropic API Key
- Go to **console.anthropic.com**
- Settings → API Keys → Create Key
- Copy the key (starts with `sk-ant-...`)

### 2. Deploy to Vercel
- vercel.com → New Project → import this folder
- Framework Preset: **Other** (it's static + serverless)
- Click Deploy

### 3. Add the API Key to Vercel
- Project dashboard → Settings → Environment Variables
- Name: `ANTHROPIC_API_KEY`
- Value: paste the key from step 1
- Apply to: Production, Preview, Development (all)
- **Redeploy** the project (Deployments tab → ⋯ on latest → Redeploy)

### 4. Point Your Domain
- Project Settings → Domains
- Add `bluerootsfoundation.org` and `www.bluerootsfoundation.org`
- Update DNS at your registrar with the records Vercel shows you

## Testing the AI Agents

After deploy:
- **Ask BlueRoots** — gold "Ask BlueRoots" button bottom-right of every page
- **Donor Concierge** — premium card inside the Donate section

Try asking:
- "What is the BlueRoots complex?"
- "How can I donate?"
- "Who is Hamoudiata Diakho?"

## Models Used
- **Ask BlueRoots** → Claude Haiku 4.5 (fast, cheap, friendly)
- **Donor Concierge** → Claude Sonnet 4.6 (more premium reasoning)

## Cost Estimate
At normal traffic (~100 conversations/day, mostly Ask):
- ~$1-3/day = ~$30-90/month

If costs spike, add rate limiting via Upstash Redis or Vercel KV.

## Security
- API key lives in Vercel env vars only — never in the frontend
- Input length capped at 20K chars per conversation
- CORS open for now (locked to your domain after launch if desired)
