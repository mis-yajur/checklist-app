# ✅ CheckList — Maintenance Management App
### Vercel + Supabase Deployment Guide

---

## 📁 Final File Structure
```
checklist-app/
├── index.html          ← Main web app
├── vercel.json         ← Vercel config
├── config.json         ← LOCAL DEV only (do not commit with real keys)
├── api/
│   └── config.js       ← Serverless function (serves env vars safely)
└── supabase_setup.sql  ← Run once in Supabase SQL Editor
```

---

## STEP 1 — Set Up Supabase Database

1. Go to **https://supabase.com** → Sign Up (free)
2. Click **"New Project"** → Name: `checklist` → Create
3. Wait ~2 min for project to be ready
4. Go to **SQL Editor** (left sidebar) → **New Query**
5. Open `supabase_setup.sql` → copy all → paste → click **Run**
6. You'll see 5 tables created ✅

**Get your keys:**
- Go to **Project Settings** (⚙️ gear) → **API**
- Copy:
  - `Project URL` → e.g. `https://abcdefgh.supabase.co`
  - `anon / public` key → long `eyJ...` string

---

## STEP 2 — Push to GitHub

1. Go to **https://github.com** → New Repository
2. Name: `checklist-app` → Public → Create
3. Upload these files (drag & drop or use GitHub Desktop):
   ```
   index.html
   vercel.json
   api/config.js
   supabase_setup.sql
   ```
   ⚠️ **DO NOT upload `config.json` with real keys** — it's for local dev only

---

## STEP 3 — Deploy on Vercel

1. Go to **https://vercel.com** → Sign Up with GitHub
2. Click **"Add New Project"**
3. Import your `checklist-app` GitHub repository
4. **Framework Preset:** Other (leave blank)
5. **Root Directory:** `./` (default)
6. Click **"Environment Variables"** — add these one by one:

| Variable Name       | Value                            |
|---------------------|----------------------------------|
| `SUPABASE_URL`      | `https://xxxx.supabase.co`       |
| `SUPABASE_ANON_KEY` | `eyJhbGci...` (your anon key)    |
| `ADMIN_PASS`        | `Admin@1234`                     |
| `USER_PASS`         | `User@1234`                      |
| `ADMIN_USER`        | `admin`                          |

7. Click **"Deploy"** → wait ~1 minute
8. Your app is live at: `https://checklist-app.vercel.app` 🎉

---

## STEP 4 — Update After Changes

Any time you push to GitHub → Vercel **auto-redeploys** in ~30 seconds.

To update env variables:
- Vercel Dashboard → Project → **Settings → Environment Variables**
- Edit → Save → **Redeploy**

---

## 🔑 Login Credentials

| Role  | Username          | Password     |
|-------|-------------------|--------------|
| Admin | `admin`           | `Admin@1234` |
| User  | (name from Doers) | `User@1234`  |

---

## 💻 Local Development

For testing on your computer:

1. Edit `config.json` — paste your real Supabase keys:
```json
{
  "supabase_url":      "https://xxxx.supabase.co",
  "supabase_anon_key": "eyJ...",
  "app": {
    "ADMIN_PASS": "Admin@1234",
    "USER_PASS":  "User@1234"
  }
}
```

2. Install a simple local server:
```bash
npx serve .
```
Or just open with VS Code → Live Server extension

3. Open `http://localhost:3000`

---

## 📊 Scoring Formula

```
Score = (Tasks Done On Time ÷ Total Tasks Done × 100) − 100
```

| Performance        | Score |
|--------------------|-------|
| 100% on time       | 0     |
| 80% on time        | −20   |
| 50% on time        | −50   |
| 0% on time (all late) | −100 |

**Higher score = better performance. Maximum possible score = 0**

---

## 🛠 Troubleshooting

| Problem | Fix |
|---------|-----|
| "Config not found" error | Check env vars are set in Vercel Dashboard |
| Login fails for User | Make sure doer name in DB matches exactly |
| Tables missing | Re-run `supabase_setup.sql` in Supabase SQL Editor |
| Data not loading | Check Supabase → Table Editor → verify tables exist |
| CORS error | In Supabase → API Settings → add your Vercel URL to allowed origins |
