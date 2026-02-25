# Hosting Arivu Systems on GitHub Pages — Detailed Guide

This guide walks you through hosting the Arivu Systems static website on GitHub Pages, including optional custom domain setup (e.g. **arivusystems.com**).

---

## Table of Contents

1. [Prerequisites](#1-prerequisites)
2. [Push Your Code to GitHub](#2-push-your-code-to-github)
3. [Enable GitHub Pages](#3-enable-github-pages)
4. [Your Site URLs](#4-your-site-urls)
5. [Custom Domain](#5-custom-domain)
6. [Enforce HTTPS](#6-enforce-https)
7. [Updating Your Site](#7-updating-your-site)
8. [Troubleshooting](#8-troubleshooting)

---

## 1. Prerequisites

Before you start, ensure you have:

| Requirement | Details |
|-------------|--------|
| **GitHub account** | Sign up at [github.com](https://github.com) if you don’t have one. |
| **Git** | Installed on your machine ([git-scm.com](https://git-scm.com)). |
| **Repository** | Your Arivu Systems project in a Git repo (this folder). |
| **Domain (optional)** | If using a custom domain (e.g. **arivusystems.com**), you need control over that domain’s DNS. |

---

## 2. Push Your Code to GitHub

### 2.1 Create a new repository on GitHub

1. Go to [github.com](https://github.com) and sign in.
2. Click the **+** (top right) → **New repository**.
3. Set:
   - **Repository name:** e.g. `arivu-systems` or `arivusystems` (your choice).
   - **Description:** optional (e.g. “Arivu Systems website”).
   - **Visibility:** **Public** (required for free GitHub Pages).
   - Do **not** check “Add a README” if your project already has files.
4. Click **Create repository**.

### 2.2 Push your local project to GitHub

If the project is **not** yet a Git repo:

```bash
cd /path/to/arivu-systems
git init
git add .
git commit -m "Initial commit: Arivu Systems website"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
git push -u origin main
```

If it **is** already a Git repo and you only need to add GitHub as remote and push:

```bash
cd /path/to/arivu-systems
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
git branch -M main
git push -u origin main
```

Replace `YOUR_USERNAME` with your GitHub username and `YOUR_REPO_NAME` with the repository name you chose.

---

## 3. Enable GitHub Pages

1. Open your repository on GitHub.
2. Go to **Settings** (tab in the repo).
3. In the left sidebar, under **“Code and automation”**, click **Pages**.
4. Under **“Build and deployment”**:
   - **Source:** choose **Deploy from a branch**.
   - **Branch:** select the branch that has your site (e.g. `main` or `solution-16jan`).
   - **Folder:** select **/ (root)**.
5. Click **Save**.

GitHub will build and deploy your site. The first time can take 1–2 minutes.

---

## 4. Your Site URLs

After deployment:

| Type | URL |
|------|-----|
| **Default GitHub Pages** | `https://YOUR_USERNAME.github.io/YOUR_REPO_NAME/` |
| **With custom domain** (after setup) | `https://arivusystems.com` (and optionally `www.arivusystems.com`) |

Example: if your username is `johndoe` and repo is `arivu-systems`, the default URL is:

`https://johndoe.github.io/arivu-systems/`

You can find the exact URL under **Settings → Pages** after the first deployment.

---

## 5. Custom Domain (arivusystems.com)

Your repo already contains a **CNAME** file with `arivusystems.com`. That tells GitHub Pages to serve the site at that domain once DNS is correct.

### 5.1 Add the custom domain in GitHub

1. **Settings → Pages**.
2. Under **“Custom domain”**, type: **arivusystems.com**.
3. Click **Save**.
4. Wait for GitHub to verify. If it shows a DNS warning, continue with the DNS steps below.

### 5.2 Configure DNS at your domain registrar

You need to point **arivusystems.com** (and optionally **www.arivusystems.com**) to GitHub Pages.

Log in to where you manage DNS for **arivusystems.com** (e.g. GoDaddy, Namecheap, Cloudflare, Google Domains).

#### Option A: Apex domain (arivusystems.com) — recommended

Add **A records** so that `arivusystems.com` points to GitHub’s IPs:

| Type | Host / Name | Value / Points to | TTL |
|------|-------------|-------------------|-----|
| A    | `@` (or blank) | `185.199.108.153` | 3600 |
| A    | `@` (or blank) | `185.199.109.153` | 3600 |
| A    | `@` (or blank) | `185.199.110.153` | 3600 |
| A    | `@` (or blank) | `185.199.111.153` | 3600 |

Some registrars only allow one A record per IP; add four separate A records, one per IP.

#### Option B: www subdomain (www.arivusystems.com)

To serve the site at **www.arivusystems.com**:

| Type  | Host / Name | Value / Points to              | TTL  |
|-------|-------------|---------------------------------|------|
| CNAME | `www`       | `YOUR_USERNAME.github.io`       | 3600 |

Replace `YOUR_USERNAME` with your GitHub username.

If you use **both** apex and www:

- Keep the four A records for `arivusystems.com`.
- Add the CNAME for `www` as above.
- In **Settings → Pages**, you can set the custom domain to either `arivusystems.com` or `www.arivusystems.com`. GitHub will redirect the other if you enable **Enforce HTTPS** and use their default behavior.

### 5.3 Keep the CNAME file in your repo

Your project already has:

```
CNAME
```

Content: **arivusystems.com** (one line, no `https://` or path).

- Do **not** delete this file.
- If you use **www** as the primary domain, change the content to `www.arivusystems.com` and ensure DNS has the CNAME for `www` as in Option B.

### 5.4 Wait for DNS and GitHub verification

- DNS can take from a few minutes up to 48 hours (often 10–30 minutes).
- In **Settings → Pages**, the **Custom domain** section will show when the domain is verified.
- After it’s verified, enable **Enforce HTTPS** (see below).

---

## 6. Enforce HTTPS

1. Go to **Settings → Pages**.
2. Under **Custom domain**, ensure the domain is verified (no warning).
3. Check **Enforce HTTPS**.

Visitors will be redirected from `http://` to `https://`. If **Enforce HTTPS** is greyed out, wait for DNS/certificate provisioning (can take up to 24 hours for new domains).

---

## 7. Updating Your Site

Every push to the branch you selected for GitHub Pages triggers a new deployment.

```bash
cd /path/to/arivu-systems
git add .
git commit -m "Update content or fix"
git push origin main
```

Replace `main` with your Pages branch if different. The site usually updates within 1–3 minutes. You can check **Settings → Pages** for deployment status, or the **Actions** tab if you add a workflow later.

---

## 8. Troubleshooting

### 404 or “There isn’t a GitHub Pages site here”

- Confirm **Settings → Pages** has **Source: Deploy from a branch** and the correct **branch** and **/ (root)**.
- Ensure **index.html** is in the **root** of that branch (not inside a subfolder).
- Wait 2–5 minutes after the first enable and refresh.

### Pages work at github.io but not at arivusystems.com

- Confirm the **CNAME** file in the repo contains only `arivusystems.com` (or `www.arivusystems.com`) and is on the same branch used for Pages.
- Verify DNS: run `dig arivusystems.com` or use [https://dnschecker.org](https://dnschecker.org) and check that the A records (or CNAME for www) match the values in section 5.
- In **Settings → Pages**, remove the custom domain, save, then re-add it and save again to retrigger verification.

### CSS, JS, or images don’t load (broken layout or 404s)

- Use **relative paths** in HTML (e.g. `assets/css/style.css`, not `/assets/...` from a different context). This project already uses relative paths, so it should work.
- Open the live site URL and check the browser **Network** tab for failed requests; fix any wrong paths (e.g. typos, wrong folder).

### Custom domain shows “Certificate not ready” or HTTPS error

- Leave **Enforce HTTPS** off until the domain is verified and the certificate is active (can take up to 24 hours).
- Ensure you did not add a CNAME for the **apex** domain (e.g. `arivusystems.com`); apex must use **A** records. CNAME is only for **www**.

### Wrong branch or folder selected

- **Settings → Pages** → change **Branch** and/or **Folder** → **Save**. GitHub will redeploy from the new choice.

---

## Quick reference

| Step | Action |
|------|--------|
| 1 | Create repo on GitHub, push your code (branch e.g. `main`). |
| 2 | **Settings → Pages** → Source: **Deploy from a branch** → Branch: **main** → Folder: **/ (root)** → Save. |
| 3 | Use default URL: `https://USERNAME.github.io/REPO_NAME/`. |
| 4 | (Optional) **Custom domain:** set `arivusystems.com` in Settings → Pages; add A (and optionally www CNAME) records at your DNS; keep **CNAME** file in repo. |
| 5 | When domain is verified, enable **Enforce HTTPS**. |
| 6 | Updates: push to the same branch; site refreshes in 1–3 minutes. |

For general project and local run instructions, see **[DOCUMENTATION.md](./DOCUMENTATION.md)**.
