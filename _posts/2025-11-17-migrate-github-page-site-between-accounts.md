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
