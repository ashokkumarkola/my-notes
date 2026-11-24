---
tags:
  - cheat-sheet
  - tools
  - mkdocs
---

# MkDocs Cheat Sheet

## Commands

```bash
source .venv/bin/activate
pip install -r requirements.txt
mkdocs serve                       # http://127.0.0.1:8000
mkdocs serve -a 127.0.0.1:8001     # other port
mkdocs build --strict              # fail on warnings
mkdocs --version
```

## Files

| File | Role |
|---|---|
| `mkdocs.yml` | Config: theme, nav, extensions |
| `docs/` | All pages (`.md`) |
| `docs/**/index.md` | Section landing page |
| `requirements.txt` | Python deps |
| `site/` | Build output, git-ignored |

## Add a page

```bash
touch docs/section/topic.md          # 1. create: tags front matter + "# Title"
# 2. add to nav in mkdocs.yml
# 3. new tag? add to tags_allowed
mkdocs build --strict                # 4. verify
```

```yaml
nav:
  - Section:
      - section/index.md
      - Topic: section/topic.md
```

## Move a page

```bash
git mv docs/a/x.md docs/b/x.md
grep -rn "x.md" docs/ mkdocs.yml     # fix links + nav
mkdocs build --strict
```

## Syntax quick ref

| Need | Syntax |
|---|---|
| Link page | `[Text](../other/page.md)` |
| Link heading | `[Text](page.md#heading-id)` |
| Image | `![alt](images/x.png)` |
| Code | ```` ```bash ```` … ```` ``` ```` |
| Callout | `!!! note "Title"` + 4-space indent |
| Collapsible | `??? tip "Title"` |
| Tabs | `=== "Linux"` + 4-space indent |
| Keys | `++ctrl+c++` |

Full syntax: [Format guide](mkdocs-format-guide.md). Live render: [Format demo](format-demo.md).

## Common errors

| Error | Fix |
|---|---|
| `not included in the "nav"` | Add page to `nav` |
| `... which is not found` | Wrong path in `nav` |
| `no such anchor` | Fix `#heading` slug |
| `Tags not in allow list: x` | Fix typo or add tag to `tags_allowed` |
| `Address already in use` | Other `mkdocs serve` running |

## Related

- [Setup guide](mkdocs-setup-guide.md)
- [Format demo](format-demo.md)
- [Conventions](conventions.md)
- [Git](../git/cheat-sheet.md)
