
## Phase 1: Local setup

**1. Check Python (3.10 or newer needed)**
```bash
python3 --version
```
If `venv` creation fails later with `ensurepip is not available`, run `sudo apt install python3-venv`.

**2. Create and activate the virtual env**
```bash
python3 -m venv .venv
source .venv/bin/activate
```
Your prompt now shows `(.venv)`. Run `deactivate` to leave it.

**3. Create `requirements.txt`**
```text
mkdocs-material
```
Then install it:
```bash
pip install -r requirements.txt
mkdocs --version
```

**4. Create `.gitignore`**
```gitignore
.venv/
site/
__pycache__/
```

**5. Create a minimal `mkdocs.yml` in the repo root**
```yaml
site_name: My Knowledge Base
docs_dir: docs
theme:
  name: material
```
Do not add `nav` yet. Without `nav`, MkDocs builds the sidebar from the folder structure automatically.

**6. Create `docs/index.md`.** Without it, the home page shows 404.
```markdown
# My Knowledge Base

Personal technical notes.
```

**7. Run the local server**
```bash
mkdocs serve
```
Open http://127.0.0.1:8000. Press `Ctrl+C` to stop.

**Expected results**
- The site loads with the Material theme.
- The sidebar shows the `CLOUD`, `GIT`, `LEARN` and other folders, still uppercase. Phase 2 fixes that.
- `terminal.bash` and `commandprompt.cmd` do not show. Expected: only `.md` files become pages.
- The terminal may show warnings. Note them, do not fix them yet.

**8. Check the production build**
```bash
mkdocs build
```
Output goes to `site/`. Run `git status`: `site/` and `.venv/` must not appear, because `.gitignore` hides them.

**9. Commit Phase 1**
```bash
git add .gitignore requirements.txt mkdocs.yml docs/index.md
git commit -m "chore: add minimal mkdocs material setup"
```

**Why each file exists**
- `.venv/`: keeps Python packages separate from system Python.
- `requirements.txt`: lets you rebuild the same environment on another machine or in CI (Phase 7).
- `.gitignore`: keeps generated output and the venv out of Git.
- `mkdocs.yml`: the site config. It grows in Phase 3.

Paste any error or warning here. Then we go to Phase 2.