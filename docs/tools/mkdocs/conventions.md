---
tags:
  - guide
  - tools
  - mkdocs
---

# Conventions

Rules that keep this knowledge base consistent. Check before adding or moving files.

## File and folder names

| Rule | Good | Bad |
|---|---|---|
| Lowercase | `git-commands.md` | `Git-Commands.md` |
| Hyphens, no spaces/underscores | `add-ssh-keys.md` | `add ssh_keys.md` |
| Short, specific | `vpc-peering.md` | `notes-about-vpc-peering-in-aws.md` |
| Only `.md` for notes | `terminal.md` | `terminal.bash` |

## Folder structure

Rule: **folder under `docs/` = top tab. Subfolder = guide group inside that tab.**

```text
docs/
├── index.md                     ← homepage
├── <category>/                  ← top tab
│   ├── index.md                 ← category landing (required)
│   ├── cheat-sheet.md           ← optional: category-wide quick ref
│   └── <topic>/                 ← guide group in sidebar
│       ├── index.md             ← topic landing (required)
│       ├── cheat-sheet.md       ← quick ref (commands, tables)
│       └── <subtopic>.md        ← full notes
└── assets/
    └── images/                  ← shared images
```

Current categories:

```text
cloud/        aws, azure
languages/    python, javascript, java
frameworks/   react, fastapi
databases/    sql, psql, mongodb
fullstack/    backend, frontend
os/           ubuntu, windows
ide/          vscode
genai/        prompts, langchain
tools/        git, figma, mkdocs
```

- Every folder has `index.md`. Every topic has `cheat-sheet.md`.
- Max depth: 3 levels under `docs/`. Deeper = hard to navigate.
- New topic folder → create `index.md` + `cheat-sheet.md` → add topic tag to `tags_allowed` → add both to `nav`.
- New category = new top tab. Add only when at least 1 real topic exists.
- Topic file > ~300 lines or many independent subtopics → split into files in same folder.

### Page roles

| File | Holds | Style |
|---|---|---|
| `index.md` | What it is (1 line) + table of pages | Links only |
| `cheat-sheet.md` | Commands, tables, syntax | No theory, no long sentences |
| `<subtopic>.md` | Full notes, explanations | [Note template](note-template.md) |

## Pages

- Line 1: one `# Title`. Title Case.
- Line 3: one-line summary.
- Start from a [template](note-template.md).
- Headings in order: `##` → `###` → `####`. No skipped levels.
- Commands always in fenced blocks with a language.

## Tags

Front matter at very top of page:

```yaml
---
tags:
  - cheat-sheet      # 1 page type
  - databases        # 1 category = docs/ folder
  - postgresql       # 1+ topic
  - sql              # optional cross-topic
---
```

| Kind | Allowed |
|---|---|
| Page type (exactly 1) | `cheat-sheet` · `notes` · `guide` · `roadmap` · `prompt` |
| Category (exactly 1) | `cloud` · `languages` · `frameworks` · `databases` · `fullstack` · `os` · `ide` · `genai` · `tools` |
| Topic (1–3) | `aws` `azure` `python` `javascript` `java` `react` `fastapi` `sql` `postgresql` `mongodb` `backend` `frontend` `ubuntu` `windows` `vscode` `langchain` `git` `figma` `mkdocs` |

Rules:

- Lowercase, hyphens. 2–5 tags per page.
- `index.md` pages: no tags (link lists only).
- Only tags in `tags_allowed` (`mkdocs.yml`). Typo → build error.
- New topic folder → add its topic tag to `tags_allowed` + this table.
- Browse all: [Tags](../../tags.md).

## Related links

End every cheat sheet and note with:

```markdown
## Related

- [Sibling topic](../sibling/cheat-sheet.md)
- [Cross-category topic](../../category/topic/cheat-sheet.md)
```

2–4 links: siblings first, then cross-category (FastAPI ↔ Python ↔ Backend).

## Links

- Relative paths to `.md` files: `[SSH](../git/add-ssh-keys.md)`.
- No duplicate notes. One canonical page, link from others.
- External facts → link official docs in `## References`.

## Images

- Page-specific → `images/` next to the page.
- Shared → `docs/assets/images/`.
- Names: lowercase-hyphen, descriptive: `vpc-peering-flow.svg`.
- Diagrams: Mermaid first, `.svg` second, `.png` for screenshots only.
- Always alt text.

## Moving and renaming

```bash
git mv old/path.md new/path.md     # never plain mv
grep -rn "path.md" docs/           # find links to fix
mkdocs build --strict              # confirm no broken links
```

- Commit renames separately from content edits.
- Published pages: renaming breaks URLs. Add redirects (Phase 8).

## Git

### Commit messages

Format: `<type>: <short summary>`, lowercase, imperative.

| Type | Use for | Example |
|---|---|---|
| `docs` | Add or edit notes | `docs: add aws iam notes` |
| `refactor` | Move, rename, restructure | `refactor: split aws into service pages` |
| `chore` | Config, deps, tooling | `chore: pin mkdocs below 2.0` |
| `ci` | GitHub Actions | `ci: add pages deploy workflow` |
| `fix` | Broken link, wrong info | `fix: correct s3 storage class table` |
| `style` | Theme, CSS, layout | `style: add dark mode toggle` |

### Branches

- `main` = published site. Every push to `main` deploys.
- `dev` or `<topic>` branch for big changes. Merge when `mkdocs build --strict` passes.

### Before every commit

```bash
mkdocs build --strict
git status                 # no site/, no .venv/, no secrets
git diff --staged
```

## Never commit

- API keys, access keys, tokens, passwords, `.env` files.
- Private hostnames, IPs, account IDs, internal company info.
- `site/`, `.venv/`, `__pycache__/`.

!!! danger "Public repo = public notes"
    Anything pushed to a public repo is readable by anyone and stays in Git history even after deletion. Rotate any secret that was ever pushed.
