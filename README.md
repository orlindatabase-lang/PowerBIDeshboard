# Power BI Portal — CI/CD Setup Guide

## Project Structure
```
powerbi-portal/
├── index.html              ← Your portal (main file)
├── vercel.json             ← Vercel deployment config
├── .github/
│   └── workflows/
│       └── deploy.yml      ← GitHub Actions CI/CD pipeline
└── README.md
```

---

## Step 1 — Push to GitHub

1. Go to https://github.com and create a **new repository** (e.g. `powerbi-portal`)
2. On your PC, open a terminal in this project folder and run:

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/powerbi-portal.git
git push -u origin main
```

---

## Step 2 — Connect to Vercel

1. Go to https://vercel.com and sign in (use your GitHub account)
2. Click **"Add New Project"**
3. Import your `powerbi-portal` GitHub repository
4. Vercel will auto-detect it as a static site
5. Click **Deploy** — your site will be live at `https://powerbi-portal.vercel.app`

---

## Step 3 — Get Vercel Secrets for GitHub Actions

You need 3 values from Vercel to enable automatic deployments:

### Get VERCEL_TOKEN
1. Go to https://vercel.com/account/tokens
2. Click **Create Token**
3. Name it `github-actions`, copy the token

### Get VERCEL_ORG_ID and VERCEL_PROJECT_ID
1. Install Vercel CLI on your PC:
   ```bash
   npm install -g vercel
   ```
2. Run inside your project folder:
   ```bash
   vercel link
   ```
3. This creates a `.vercel/project.json` file — open it and copy:
   - `orgId` → this is your `VERCEL_ORG_ID`
   - `projectId` → this is your `VERCEL_PROJECT_ID`

---

## Step 4 — Add Secrets to GitHub

1. Go to your GitHub repo → **Settings** → **Secrets and variables** → **Actions**
2. Click **New repository secret** and add these 3 secrets:

| Secret Name        | Value                        |
|--------------------|------------------------------|
| `VERCEL_TOKEN`     | Token from Step 3            |
| `VERCEL_ORG_ID`    | orgId from `.vercel/project.json` |
| `VERCEL_PROJECT_ID`| projectId from `.vercel/project.json` |

---

## Step 5 — Test CI/CD

Make any change to `index.html`, then:

```bash
git add .
git commit -m "Update portal"
git push
```

Go to your GitHub repo → **Actions** tab — you will see the deployment running.
In 30–60 seconds your live site at Vercel will be updated automatically. ✅

---

## Your Live URLs

After setup your site will be available at:
- **Main portal (Admin):** `https://your-project.vercel.app`
- **Department link example:** `https://your-project.vercel.app?dept=hr`

---

## Making Changes

Whenever you want to update the portal:
1. Edit `index.html`
2. Run:
   ```bash
   git add .
   git commit -m "Your change description"
   git push
   ```
3. Vercel auto-deploys in ~30 seconds ✅
