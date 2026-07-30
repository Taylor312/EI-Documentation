---
title: About this site
layout: default
parent: Reference
nav_order: 6
---

# About this site

This is the documentation site for **Easy Inspection**, built with [Just the Docs](https://just-the-docs.github.io/just-the-docs/) and published through GitHub Pages.

- Source: [github.com/Taylor312/EI-Documentation](https://github.com/Taylor312/EI-Documentation)
- Published at: [taylor312.github.io/EI-Documentation](https://taylor312.github.io/EI-Documentation/)

The **Need help? Read the documentation** link in the application points here.

## How the site is organized

| Section | Audience |
|---|---|
| [Overview]({{ site.baseurl }}/overview/) | Anyone deciding whether and how to deploy the product |
| [Setup and integration]({{ site.baseurl }}/setup/) | Integrators commissioning a cell |
| [Reference]({{ site.baseurl }}/reference/) | Integrators looking something up |
| [Operator manual]({{ site.baseurl }}/operator/) | Line operators on a finished station |

## Editing

Pages are Markdown files at the repository root. Front matter controls the title and where the page appears in the sidebar:

```yaml
---
title: Connect the robot
layout: default
parent: Setup and integration
nav_order: 3
---
```

`parent` must match a category page's `title` exactly. `nav_order` sets the position within that category.

Every page has an **Edit this page on GitHub** link at the bottom.

### Internal links

Use the site base URL so links work from both root-level pages and category pages:

```markdown
[Modbus setup]({% raw %}{{ site.baseurl }}{% endraw %}/modbus.html)
```

### Callouts

```markdown
{% raw %}{: .warning }{% endraw %}
Text that must not be missed.

{% raw %}{: .note }{% endraw %}
Supplementary information.

{% raw %}{: .screenshot }{% endraw %}
Screenshot: description of the image, with a red box around the thing that matters.
```

## Screenshot placeholders

Screenshot callouts mark where an annotated image belongs. They render as a dashed cyan box so they are obvious in a draft and easy to find.

The convention is one sentence naming the screen and what the red box highlights. To replace one, swap the callout for the image:

```markdown
![Robot settings panel with Assert API control highlighted]({% raw %}{{ site.baseurl }}{% endraw %}/assets/images/connect-assert-control.png)
```

Put images under `assets/images/` and name them after the page they belong to.

## Local preview

Requires Ruby with the DevKit. Once installed:

```powershell
cd "C:\MasterData\Projects\Walter\Easy Inspection Documentation"
bundle install
bundle exec jekyll serve --livereload
```

Then open <http://127.0.0.1:4000/EI-Documentation/>.

Markdown and stylesheet edits reload automatically. Changes to `_config.yml` require restarting the server.

## Publishing

Pushing to `main` triggers a GitHub Actions workflow that builds the site and deploys it to GitHub Pages. The repository's Pages source must be set to **GitHub Actions**.
