**Phases**

0. **Safety checkpoint.** Commit or stash the current uncommitted work, so each phase has a clean diff to review or roll back.
1. **Local setup.** Create `.venv`, add `requirements.txt` with `mkdocs-material`, add a `.gitignore` for `.venv/` and `site/`. Run `mkdocs serve` with a minimal `mkdocs.yml` to prove it works.
2. **Restructure notes.** Rename folders and files to lowercase kebab-case (for example `docs/cloud/aws/`). Use `git mv` so history is kept. Convert `.bash` and `.cmd` notes to `.md` with fenced code blocks. Add an `index.md` to each section.
3. **Configure `mkdocs.yml`.** Set up the theme, light/dark palette, top tabs, sidebar, right-hand TOC, search and an explicit `nav`.
4. **Markdown extensions.** Turn on code highlighting with copy buttons, admonitions, collapsible blocks, tabs, Mermaid and task lists.
5. **Homepage and about page.** Write `docs/index.md` as a dashboard of categories, plus `about.md`.
6. **Content polish.** Apply the note template, split big files (for example one page per service instead of one large `aws.md`), add tags and related links. Check that no secrets are committed.
7. **Deploy.** Add `.github/workflows/deploy.yml`, set Settings → Pages → Source to GitHub Actions, push and check the live URL.
8. **Optional extras.** Custom domain, plus plugins for last-updated dates, page redirects and a blog.

**Before Phase 7:** a public repo means every note is public. Decide whether this repo should be public or private.

**Method to reuse next time**
1. Read the source of truth first (here, the guide's roadmap in section 15).
2. List what the repo has against what the target needs.
3. Order phases so each one leaves a working state you can check (`mkdocs serve` builds without errors).
4. Make one commit per phase.
