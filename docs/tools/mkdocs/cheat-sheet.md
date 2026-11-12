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
touch docs/section/topic.md          # 1. create, add "# Title"
# 2. add to nav in mkdocs.yml
mkdocs build --strict                # 3. verify
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

Full syntax: [Format guide](mkdocs-format-guide.md).

## Common errors

| Error | Fix |
|---|---|
| `not included in the "nav"` | Add page to `nav` |
| `... which is not found` | Wrong path in `nav` |
| `no such anchor` | Fix `#heading` slug |
| `Address already in use` | Other `mkdocs serve` running |
