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

```text
docs/
├── index.md                 ← homepage
├── <category>/              ← top tab: cloud, git, os, learn ...
│   ├── index.md             ← section landing page (required)
│   ├── <topic>.md           ← one topic = one file
│   └── <big-topic>/         ← topic grows → own folder
│       ├── index.md
│       └── <subtopic>.md
└── assets/
    └── images/              ← shared images
```

- Every folder has `index.md`.
- Max depth: 3 levels under `docs/`. Deeper = hard to navigate.
- New category only when at least 1 real note exists.
- Topic file > ~300 lines or many independent subtopics → split into folder.

## Pages

- Line 1: one `# Title`. Title Case.
- Line 3: one-line summary.
- Start from a [template](note-template.md).
- Headings in order: `##` → `###` → `####`. No skipped levels.
- Commands always in fenced blocks with a language.

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
- After Phase 7, renaming published pages breaks URLs. Add redirects (Phase 8).

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

- `main` = published site (after Phase 7).
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
