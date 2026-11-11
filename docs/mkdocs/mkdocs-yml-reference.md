# mkdocs.yml Reference

Every `mkdocs.yml` key used in this site, one line each. Status: **Active** = in config now, **Phase N** = added in that phase.

Official reference: [MkDocs config](https://www.mkdocs.org/user-guide/configuration/) · [Material setup](https://squidfunk.github.io/mkdocs-material/setup/)

## Current config

```yaml
site_name: My Knowledge Base
docs_dir: docs
theme:
  name: material
```

---

## Site info

| Key | Purpose | Status |
|---|---|---|
| `site_name` | Title in header and browser tab | Active |
| `site_description` | Meta description for search engines | Phase 3 |
| `site_author` | Meta author | Phase 3 |
| `site_url` | Final public URL. Needed for sitemap, canonical links | Phase 7 |
| `copyright` | Footer text | Phase 3 |

## Repository

| Key | Purpose | Status |
|---|---|---|
| `repo_url` | GitHub link + icon in header | Phase 7 |
| `repo_name` | Label next to repo icon | Phase 7 |
| `edit_uri` | "Edit this page" target, e.g. `edit/main/docs/` | Phase 7 |

## Build

| Key | Purpose | Status |
|---|---|---|
| `docs_dir` | Source folder. Default `docs` | Active |
| `site_dir` | Output folder. Default `site` | Default |
| `exclude_docs` | Files in `docs/` to skip, gitignore syntax | As needed |
| `not_in_nav` | Pages built but hidden from nav, no warning | As needed |
| `validation` | Warning level for links, nav, anchors | Phase 3 |

## Navigation

| Key | Purpose | Status |
|---|---|---|
| `nav` | Explicit menu order. Omit = auto from folders | Phase 3 |

```yaml
nav:
  - Home: index.md
  - Cloud:                    # top tab
      - cloud/index.md        # section landing (needs navigation.indexes)
      - AWS: cloud/aws/index.md
```

Paths are relative to `docs_dir`. Every path must exist.

## Theme

| Key | Purpose | Status |
|---|---|---|
| `theme.name` | `material` | Active |
| `theme.language` | UI language, e.g. `en` | Phase 3 |
| `theme.palette` | Colors, light/dark toggle | Phase 3 |
| `theme.font.text` / `.code` | Google Fonts names, or `false` to disable | Phase 3 |
| `theme.logo` / `theme.icon.logo` | Header logo image or icon | Phase 5 |
| `theme.favicon` | Browser tab icon | Phase 5 |
| `theme.icon.repo` | Repo icon in header | Phase 7 |
| `theme.features` | UI behaviours, see below | Phase 3 |

### Light/dark toggle

```yaml
theme:
  palette:
    - media: "(prefers-color-scheme: light)"
      scheme: default
      primary: indigo
      accent: indigo
      toggle:
        icon: material/brightness-7
        name: Switch to dark mode
    - media: "(prefers-color-scheme: dark)"
      scheme: slate
      primary: indigo
      accent: indigo
      toggle:
        icon: material/brightness-4
        name: Switch to light mode
```

### Features

| Feature | Effect | Status |
|---|---|---|
| `navigation.tabs` | Top-level sections as header tabs | Phase 3 |
| `navigation.tabs.sticky` | Tabs stay visible on scroll | Phase 3 |
| `navigation.sections` | Sidebar groups rendered as headings | Phase 3 |
| `navigation.expand` | Sidebar groups expanded by default | Optional |
| `navigation.indexes` | Folder `index.md` becomes clickable section title | Phase 3 |
| `navigation.path` | Breadcrumbs above title | Phase 3 |
| `navigation.top` | Back-to-top button | Phase 3 |
| `navigation.footer` | Previous/next links at page bottom | Phase 3 |
| `navigation.instant` | SPA-style fast page loads | Phase 3 |
| `navigation.tracking` | URL updates with current heading | Phase 3 |
| `toc.follow` | Right TOC scrolls to active heading | Phase 3 |
| `toc.integrate` | TOC inside left sidebar instead of right | Optional |
| `search.suggest` | Autocomplete in search | Phase 3 |
| `search.highlight` | Highlight search terms on result page | Phase 3 |
| `search.share` | Share-search-link button | Optional |
| `header.autohide` | Hide header on scroll down | Optional |
| `content.code.copy` | Copy button on code blocks | Phase 4 |
| `content.code.annotate` | Code annotations `# (1)!` | Phase 4 |
| `content.tabs.link` | All tabs with same label switch together | Phase 4 |
| `content.tooltips` | Styled tooltips | Phase 4 |
| `content.action.edit` | "Edit this page" button | Phase 7 |

## Markdown extensions

Full list with what each enables: [Format Guide → Extension checklist](mkdocs-format-guide.md#extension-checklist-feeds-phase-4). Added in Phase 4.

```yaml
markdown_extensions:
  - toc:
      permalink: true
  - admonition
  - pymdownx.superfences:
      custom_fences:
        - name: mermaid
          class: mermaid
          format: !!python/name:pymdownx.superfences.fence_code_format
```

## Plugins

Listing `plugins:` replaces defaults. Always include `search` again.

| Plugin | Purpose | Package | Status |
|---|---|---|---|
| `search` | Full-text search | built-in | Phase 3 |
| `tags` | Tag index pages | built into Material | Phase 6 |
| `offline` | Site works from file system | built into Material | Phase 8 |
| `git-revision-date-localized` | "Last updated" date | `mkdocs-git-revision-date-localized-plugin` | Phase 8 |
| `redirects` | Old URL → new URL after renames | `mkdocs-redirects` | Phase 8 |

Plugins with own package → add to `requirements.txt`.

## Extra

| Key | Purpose | Status |
|---|---|---|
| `extra.social` | Footer social icons + links | Phase 5 |
| `extra.generator` | `false` hides "Made with Material" | Optional |
| `extra_css` | Custom CSS files under `docs/` | Phase 8 |
| `extra_javascript` | Custom JS files under `docs/` | As needed |

---

## Gotchas

| Problem | Fix |
|---|---|
| VS Code flags `!!python/name:` as error | Add to VS Code `settings.json`: `"yaml.customTags": ["!!python/name:pymdownx.superfences.fence_code_format", "!!python/name:material.extensions.emoji.twemoji", "!!python/name:material.extensions.emoji.to_svg"]` |
| Indentation error | YAML = spaces only, 2 per level, never tabs |
| Search disappeared | Added `plugins:` without `- search` |
| `nav` page missing warning | Path wrong or file not created yet |
| Config change not applied | Restart `mkdocs serve` after editing `mkdocs.yml` if reload misses it |
