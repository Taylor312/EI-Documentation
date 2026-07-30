# Easy Inspection Documentation

Documentation site for **Easy Inspection**, built with [Just the Docs](https://just-the-docs.github.io/just-the-docs/) and published through GitHub Pages.

- GitHub: https://github.com/Taylor312/EI-Documentation
- Live site: https://taylor312.github.io/EI-Documentation/

The **Need help? Read the documentation** link in the app points at the live site.

## Structure

Markdown files at the repo root are the pages. Four category parents define the sidebar:

| Category page | Contains |
|---|---|
| `overview.md` | Introduction (`index.md`), system and control model, downloads |
| `setup.md` | The integrator commissioning sequence, in order |
| `reference.md` | Workflow summary, storage, settings, troubleshooting, safety, about |
| `operator.md` | Self-contained factory-mode operator manual |

Front matter places a page in the sidebar. `parent` must match a category page's `title` exactly.

```yaml
---
title: Connect the robot
layout: default
parent: Setup and integration
nav_order: 3
---
```

### Internal links

Use the site base URL so links resolve from both root-level pages and category pages, which have directory-style URLs:

```markdown
[Modbus setup]({{ site.baseurl }}/modbus.html)
```

### Callouts

```markdown
{: .warning }
Something that must not be missed.

{: .note }
Supplementary information.

{: .screenshot }
The Robot settings panel with a red box around Assert API control.
```

`screenshot` renders as a dashed cyan placeholder. Replace one with the real image when it is captured:

```markdown
![Robot settings with Assert API control highlighted]({{ site.baseurl }}/assets/images/connect-assert-control.png)
```

Images go under `assets/images/`, named after the page they belong to.

### Diagrams

Mermaid is enabled. Use a ```mermaid fenced block; the theme renders it with the site's dark palette (`_includes/mermaid_config.js`).

## Theming

| File | Purpose |
|---|---|
| `_sass/color_schemes/ei.scss` | Dark gunmetal + cyan palette, Oxanium type |
| `_sass/custom/setup.scss` | Callout colour variables |
| `_sass/custom/custom.scss` | Fluid layout, sidebar nav styling, callout styling |
| `_includes/head_custom.html` | Oxanium web font |

## Local preview

Requires Ruby with DevKit (one-time: `winget install RubyInstallerTeam.RubyWithDevKit.3.3`).

```powershell
cd "C:\MasterData\Projects\Walter\Easy Inspection Documentation"
bundle install
bundle exec jekyll serve --livereload
```

Open http://127.0.0.1:4000/EI-Documentation/

Markdown and `_sass/` edits reload automatically. **Changes to `_config.yml` require restarting the server.**

## Publishing

Pushing to `main` runs the **Deploy Jekyll site to Pages** workflow. One-time setup: repo **Settings** > **Pages** > **Build and deployment** > **Source** > **GitHub Actions**.
