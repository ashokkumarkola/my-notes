# My Notes

Personal technical knowledge base. Markdown notes in `docs/`, published as a website with [MkDocs](https://www.mkdocs.org) + [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/).

## Quick start

```bash
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
mkdocs serve                      # http://127.0.0.1:8000
```

## Commands

| Task | Command |
|---|---|
| Live preview | `mkdocs serve` |
| Build, fail on warnings | `mkdocs build --strict` |
| Output folder | `site/` (git-ignored) |

## Structure

```text
docs/
├── index.md         homepage dashboard
├── about.md         about this site
├── tags.md          tag index (auto)
├── assets/          favicon, shared images
├── cloud/           AWS, Azure
├── languages/       Python, JavaScript, Java
├── frameworks/      React, FastAPI
├── databases/       SQL, PostgreSQL, MongoDB
├── fullstack/       Backend, frontend
├── os/              Ubuntu, Windows
├── ide/             VS Code
├── genai/           Prompts, LangChain
└── tools/           Git, Figma, MkDocs
mkdocs.yml           site config + navigation
requirements.txt     Python dependencies
```

Each folder: `index.md` (landing) + `cheat-sheet.md` (quick reference).

## Add a note

1. Create `docs/<category>/<topic>/<note>.md` with a `# Title`.
2. Add it to `nav` in `mkdocs.yml`.
3. Run `mkdocs build --strict`.

Guides: [setup](docs/tools/mkdocs/mkdocs-setup-guide.md) · [format](docs/tools/mkdocs/mkdocs-format-guide.md) · [conventions](docs/tools/mkdocs/conventions.md) · [templates](docs/tools/mkdocs/note-template.md)
