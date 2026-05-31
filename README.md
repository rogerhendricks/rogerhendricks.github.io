# KeepOnPacing Blog

Welcome to the modernized **KeepOnPacing** cardiac blog! This site has been completely upgraded to run on the latest version of Hugo with the high-performance, responsive, and dark-mode-first **Congo** theme.

---

## 📂 File Structure Breakdown

The directory tree below outlines the modern, modular structure of the repository:

```text
.
├── config/
│   └── _default/
│       ├── hugo.toml             # Core site settings and theme selection
│       ├── params.toml           # Theme styling, search, and footer controls
│       ├── languages.en.toml     # Bio, header branding, and author details
│       ├── markup.toml           # Markdown rendering (tables, math formulas)
│       └── menus.en.toml         # Navigation header menus
├── assets/
│   ├── css/
│   │   └── schemes/
│   │       └── emerald.css       # Custom emerald/teal color scheme
│   └── img/
│       └── heartbeat.svg         # Glowing ECG pacing spike SVG logo
├── content/
│   └── posts/
│       └── companies-view-of-time.md  # Modernized pacemaker timing post
├── layouts/
│   └── _partials/
│       └── logo.html             # SVG logo override template (safeguards build)
├── static/                       # Holds static resources served at root
├── themes/
│   └── congo/                    # Congo theme core files (Git Submodule)
└── .github/
    └── workflows/
        └── gh-pages.yml          # Upgraded automated CI/CD deployment pipeline
```

---

## ✍️ How to Write a Post

All posts are written in standard Markdown and stored as `.md` files inside the `content/posts/` directory.

### Step 1: Create a New Post File
To create a new post, either copy an existing one or run the standard Hugo command in your project directory:
```bash
# Using the Hugo CLI tool
hugo new posts/your-post-title.md
```
Alternatively, you can manually create a new file named `your-post-title.md` inside `content/posts/`.

---

## 🏷️ Post Parameters (Front Matter)

Every post requires a block of metadata at the very top, enclosed in triple-dashes `---`. This is called **Front Matter** and controls the title, date, URL, search tags, and categories.

Here is a template copy of a standard post front matter:

```yaml
---
title: "Your Post Title Here"
date: 2026-05-31T11:00:00+10:00
description: "A short, professional description of the article for search results and social cards."
summary: "An engaging 1-2 sentence hook displayed on the homepage list."
showTableOfContents: true

# Taxonomies
categories: ["Device Technical"]
tags: ["pacemakers", "cardiology", "clinical"]
---
```

### Explaining the Parameters:

* **`title`:** The main headline of the post (appears at the top of the article and in search results).
* **`date`:** The date/time of the article. Used to order posts on the homepage.
* **`description`:** High-value SEO description.
* **`summary`:** A brief hook snippet displayed on card-lists. If left blank, Hugo will auto-generate one from the post's first paragraph.
* **`showTableOfContents`:** Set to `true` to dynamically render a gorgeous, clickable table of contents on the side (highly recommended for longer technical posts).
* **`categories`:** Broad groupings of your content (e.g. `["Device Technical"]`, `["Clinical Cases"]`, `["Electrophysiology"]`). Displays in the "Categories" tab.
* **`tags`:** Specific keywords/topics within your articles (e.g. `["pacemakers"]`, `["biotronik"]`, `["ventricular-safety-pacing"]`). Useful for reader filtering.

---

## 🚀 Publishing Your Post

Once you have written your post, simply commit the new file and push it to GitHub:

```bash
# 1. Stage the new post
git add content/posts/your-post-title.md

# 2. Commit the new post
git commit -m "Added post: Your Post Title Here"

# 3. Publish to the web
git push
```
Your GitHub Pages CI/CD workflow will automatically build the site and publish your new post in less than a minute!
