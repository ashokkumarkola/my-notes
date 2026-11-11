# MkDocs Setup Guide

Step-by-step setup of this knowledge base with MkDocs + Material for MkDocs, hosted on GitHub Pages.
Commands first, one-line reason after.

Related guides:

- [Format Guide](mkdocs-format-guide.md): Markdown syntax for every format
- [mkdocs.yml Reference](mkdocs-yml-reference.md): every config key, one line each
- [Note Templates](note-template.md): skeletons for new notes
- [Conventions](conventions.md): naming, structure, Git rules

## Quick reference

| Task | Command |
|---|---|
| Activate venv | `source .venv/bin/activate` |
| Leave venv | `deactivate` |
| Install deps | `pip install -r requirements.txt` |
| Live preview | `mkdocs serve` → <http://127.0.0.1:8000> |
| Preview on other port | `mkdocs serve -a 127.0.0.1:8001` |
| Build site | `mkdocs build` |
| Build, fail on warnings | `mkdocs build --strict` |
| Check version | `mkdocs --version` |

## Phases overview

| Phase | Work | Result | Status |
|---|---|---|---|
| 0 | Safety checkpoint | Clean working tree | Done |
| 1 | Local setup | Site runs locally | Done |
| 2 | Restructure notes | Lowercase paths, all `.md` | Done |
| 3 | Configure `mkdocs.yml` | Tabs, sidebar, theme, search | To do |
| 4 | Markdown extensions | Code, callouts, Mermaid | To do |
| 5 | Homepage + about | Landing dashboard | To do |
| 6 | Content polish | Template, split, tags | To do |
| 7 | Deploy | Live on GitHub Pages | To do |
| 8 | Extras | Domain, plugins | To do |

---

## Phase 0: Safety checkpoint

Goal: start every phase from a clean tree, so each phase is one reviewable diff.

```bash
git status                  # what changed
git diff                    # review edits
```

Option A, commit:

```bash
git add docs/
git commit -m "notes: <what changed>"
```

Option B, stash:

```bash
git stash push -u -m "wip"  # -u = include untracked
git stash list
git stash pop               # restore
```

Optional branch for isolated work:

```bash
git switch -c <branch-name>
```

Done when: `git status` → `nothing to commit, working tree clean`.

---

## Phase 1: Local setup

### 1. Check Python (3.10+)

```bash
python3 --version
```

### 2. Create virtual env

```bash
python3 -m venv .venv
source .venv/bin/activate   # prompt shows (.venv)
deactivate                  # leave venv
```

Why: keeps packages out of system Python.

### 3. Create `requirements.txt`

```text
mkdocs-material
mkdocs>=1.6,<2
```

Why: same environment everywhere (laptop, CI).
Why `<2`: MkDocs 2.0 breaks plugins and themes. Material stays on 1.x.

```bash
pip install -r requirements.txt
mkdocs --version
```

### 4. Create `.gitignore`

```gitignore
.venv/
site/
__pycache__/
```

Why: venv and build output never go into Git.

### 5. Create minimal `mkdocs.yml` (repo root)

```yaml
site_name: My Knowledge Base
docs_dir: docs
theme:
  name: material
```

No `nav` yet. Sidebar is built from folders automatically.

### 6. Create `docs/index.md`

```markdown
# My Knowledge Base

Personal technical notes.
```

Why: without it, home page = 404.

### 7. Run and build

```bash
mkdocs serve                # live preview, auto-reload on save
mkdocs build                # output → site/
git status                  # site/ and .venv/ must NOT appear
```

### 8. Commit

```bash
git add .gitignore requirements.txt mkdocs.yml docs/index.md
git commit -m "chore: add minimal mkdocs material setup"
```

---

## Phase 2: Restructure notes

Goal: lowercase URL-friendly paths, every note `.md`, every section has `index.md`.

### Rules

- Lowercase, hyphens, no spaces: `async-programming.md`.
- Always `git mv`, never plain `mv`. Keeps file history.
- Commit renames first, content edits second. Clean diffs.
- Big topic → folder with `index.md`: `aws.md` → `aws/index.md`. Split later without URL change.
- Only `.md` files become pages. Convert `.sh`, `.bash`, `.cmd` notes to `.md` with code fences.

### 1. Rename folders and files

```bash
git mv docs/CLOUD docs/cloud                        # Linux: one step
git mv docs/CLOUD docs/tmp && git mv docs/tmp docs/cloud   # Windows/macOS: case-only rename
git mv docs/cloud/aws/aws.md docs/cloud/aws/index.md
git mv docs/os/ubuntu/terminal.bash docs/os/ubuntu/terminal.md
```

### 2. Commit renames only

```bash
git status                  # every line = R (renamed)
git commit -m "refactor: lowercase docs paths"
```

### 3. Fix content

Converted script note → title + one fenced block:

````markdown
# Ubuntu Terminal

```bash
cd ..
ls -la
```
````

Why fence: without it, every `# comment` line renders as a heading.

Every page gets one `# Title` on line 1. Without it, MkDocs uses the filename.

### 4. Add section `index.md`

```markdown
# Git

Version control notes.

- [Git commands](git-commands.md)
- [Add SSH keys](add-ssh-keys.md)
```

Links are relative to the current file.

### 5. Verify

```bash
find docs -name '*[A-Z]*'          # expect: nothing
find docs -type f ! -name '*.md'   # expect: nothing (images allowed later)
mkdocs build --strict              # fails on broken links
```

### 6. Commit

```bash
git add -A                         # -A records moves as renames
git commit -m "docs: add section index pages, fix converted notes"
```

---

## Phase 3: Configure `mkdocs.yml`

_To do._

## Phase 4: Markdown extensions

_To do._ Required extensions per format: see [Format Guide](mkdocs-format-guide.md).

## Phase 5: Homepage + about

_To do._

## Phase 6: Content polish

_To do._

## Phase 7: Deploy to GitHub Pages

_To do._

## Phase 8: Extras

_To do._

---

## Daily workflow

```bash
source .venv/bin/activate
mkdocs serve                       # edit notes, watch browser
mkdocs build --strict              # check before commit
git add -A
git commit -m "docs: <topic>"
git push                           # Phase 7+: auto-deploys
```

## Troubleshooting

| Problem | Fix |
|---|---|
| `ensurepip is not available` | `sudo apt install python3-venv` |
| `mkdocs: command not found` | Activate venv: `source .venv/bin/activate` |
| Home page 404 | Create `docs/index.md` |
| `.sh` / `.cmd` note missing | Rename to `.md`, wrap content in code fence |
| Notes show as giant headings | Wrap script content in ```` ```bash ```` fence |
| `WARNING ... contains a link ... not found` | Fix relative path; check with `mkdocs build --strict` |
| `[Errno 98] Address already in use` | Other `mkdocs serve` running; stop it or use `-a 127.0.0.1:8001` |
| MkDocs 2.0 warning banner | Pin `mkdocs>=1.6,<2` in `requirements.txt` |
| Case rename ignored (Windows/macOS) | Two-step `git mv` through temp name |
