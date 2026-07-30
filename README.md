# Easy Inspection Documentation

Operator docs site for **Easy Inspection**, built with [Just the Docs](https://just-the-docs.github.io/just-the-docs/) and GitHub Pages.

- GitHub: https://github.com/Taylor312/EI-Documentation
- Live site (after Pages is enabled): https://taylor312.github.io/EI-Documentation/

## One-time: enable Pages

1. Repo **Settings** > **Pages**
2. **Build and deployment** > **Source** > **GitHub Actions**
3. Push `main`, or open **Actions** and re-run **Deploy Jekyll site to Pages** if needed

## Edit content

Markdown files at the repo root (`index.md`, `safety.md`, ...) become sidebar pages. Front matter controls order:

```yaml
---
title: Safety
layout: default
nav_order: 2
---
```

## Local preview

```powershell
bundle install
bundle exec jekyll serve
```

Open http://127.0.0.1:4000/EI-Documentation/
