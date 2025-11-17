---
title: "Migrate a GitHub Pages Site Between Accounts — Step-by-Step Guide"
date: 2025-11-17
categories: [GitHub Pages, DevOps & Automation]
tags: [GitHub-Pages, Migration, PAT, Git]
---

# How to Migrate a GitHub Pages Site From One Account to Another

Migrating a GitHub Pages static site from one GitHub account to another is easier than it sounds. This guide walks you through copying your site, configuring your new repository, setting up a Personal Access Token (PAT), and safely pushing updates in the future.

- **Account A** = Old GitHub account  
- **Account B** = New GitHub account  
- **Project repo** = `newblog`  
- **Final website URL**: `https://B_USERNAME.github.io/newblog`

---

## Step 0 — Create the New Repo on Account B

1. Log in to **Account B**.  
2. Create a new repository named **`newblog`**.  
3. Do **not** initialize the repo with a README, license, or `.gitignore`.  
4. If you are building a **user site**, the repo must be named:  
> B_USERNAME.github.io
5. For **project sites**, any repo name (e.g., `newblog`) is fine.

---

## Step 1 — Clone the Old Blog Repo (Account A)

From your terminal:

```bash
git clone https://github.com/A_USERNAME/A_USERNAME.github.io
```
This creates:
> A_USERNAME.github.io/

## Step 2 — Copy the Project Into a New Folder
Make a new working folder for the new account:
```bash
cp -R A_USERNAME.github.io newblog/
```

Directory structure:

newblog/

This folder will become the new GitHub Pages project under Account B.

---

## Step 3 — Remove the Old Git Remote

Inside newblog/:
```bash
cd newblog
git remote remove origin
git remote -v   # Should show nothing
```
This disconnects the folder from Account A.

---

## Step 4 — Add the New Remote (Account B)
```bash
git remote add origin https://github.com/B_USERNAME/newblog.git
```
---

## Step 5 — Switch to the main Branch
```bash
git branch -M main
```

---

## Step 6 — Create a Personal Access Token (PAT)

GitHub no longer accepts passwords when pushing.
You must use a Personal Access Token.

1. Account B → Settings
2. Developer settings → Personal access tokens
3. Click Generate new token (classic)
4. Name the token
5. Select scopes:
repo
workflow (optional)
6. Generate → Copy it somewhere safe (you can’t view it again!)

## Step 7 — Push the Site to Account B
```bash
git push -u origin main
```
Git asks:
```bash
Username: B_USERNAME
Password: <paste your PAT>
```
If you get a push rejection:
! [rejected] main -> main (fetch first)
That means GitHub auto-generated commits in the repo.

Fix:
git push -u origin main --force

## Step 8 — Enable GitHub Pages (Account B)

1. Go to **Settings → Pages** in your repository.  
2. Set the following options:  
   - **Source:** Deploy from branch  
   - **Branch:** main  
   - **Folder:** / (root)  
3. Save your changes.  

Your site will appear at:  
[https://mradelvand.github.io/soccer](https://mradelvand.github.io/soccer)
