# GIT COMMANDS SHEET

> **Git =** Version control system for tracking code changes.

---

## 1. Git Setup

```bash
git --version

git config --global user.name "Your Name"
git config --global user.email "you@example.com"

git config --global --list
git config --local --list

git config --list
```

---

## 2. Create / Start Repository

```bash
# Initialize Git in the current folder.
git init

# Clone an existing repository.
git clone <repository-url>

git clone <repository-url> <folder-name>
```

---

## 3. Check Repository

```bash
# Check current changes and branch.
git status

# View commit history.
git log
git log --oneline
git log --oneline --graph --all

# Show commit details.
git show <commit>

# Show unstaged changes.
git diff

# Show staged changes.
git diff --staged
```

---

## 4. Basic Git Flow

```text
Working Directory
       ↓
     git add
       ↓
Staging Area
       ↓
   git commit
       ↓
 Local Repository
       ↓
    git push
       ↓
Remote Repository
```

---

## 5. Add Changes

```bash
# Add all changes.
git add .

git add filename

git add folder/

# Add specific files.
git add folder/file1 folder/file2 filename

# Stage all changes.
git add -A
```

---

## 6. Commit Changes

```bash
# Create a commit.
git commit -m "message"

# Add tracked files + commit.
git commit -am "message"

# Modify the latest commit.
git commit --amend
git commit --amend -m "new message"
```

---

## 7. Branches

```bash
# List local branches.
git branch

# List local + remote branches.
git branch -a


# Create branch.
git branch <branch>

# Create + switch to branch.
git switch -c <branch>

# Switch branch.
git switch <branch>


# Delete merged branch.
git branch -d <branch>

# Force delete branch.
git branch -D <branch>

```

---

## 8. Merge

```bash
git switch main

# Merge another branch into current branch.
git merge <branch>

# Cancel merge during conflicts.
git merge --abort

# Show merged branches.
git branch --merged
```

---

## 9. Remote Repository

```bash
# Show remote URLs.
git remote -v

# Add remote repository.
git remote add origin <repository-url>

# Remove remote.
git remote remove origin

# Rename remote.
git remote rename origin upstream
```

---

## 10. Push

```bash
# Push current branch.
git push

# Push and set upstream.
git push -u origin main

# First push of a new branch.
git push -u origin <branch>

# Push specific branch.
git push origin <branch>

# Delete remote branch.
git push origin --delete <branch>
```

---

## 11. Pull

```bash
# Fetch + integrate remote changes.
git pull

# Pull specific branch.
git pull origin main

# Pull using rebase instead of merge.
git pull --rebase
```

---

## 12. Fetch

```bash
# Download remote changes without merging.
git fetch

git fetch origin

# Fetch from all remotes.
git fetch --all
```

---

## 13. Stash

```bash
# Temporarily save uncommitted changes.
git stash

# Save stash with a name.
git stash push -m "message"

# List stashes.
git stash list

# Apply latest stash + remove it.
git stash pop

# Apply latest stash without removing it.
git stash apply

# Apply specific stash.
git stash apply stash@{0}

# Delete specific stash.
git stash drop stash@{0}

# Delete all stashes.
git stash clear
```

---

## 14. Undo Changes

### Unstage File

```bash
# Remove file from staging.
git restore --staged filename
```

### Discard File Changes

```bash
# Discard uncommitted changes.
git restore filename
```

```bash
# Discard all working-directory changes.
git restore .
```

### Reset

```bash
# Unstage changes.
git reset

# Undo commit, keep changes staged.
git reset --soft HEAD~1

# Undo commit, keep changes unstaged.
git reset --mixed HEAD~1

# Undo commit and discard changes.
git reset --hard HEAD~1
```

> ⚠️ **Be careful with `--hard`.**

---

## 15. Revert

```bash
# Create a new commit that reverses another commit.
git revert <commit>

# Revert latest commit.
git revert HEAD
```

```md
> **Reset** → changes history
> **Revert** → safely creates an opposite commit
```

---

## 16. Remove Files

```bash
# Delete file + stage deletion.
git rm filename

# Delete folder + stage deletion.
git rm -r folder/

# Remove from Git but keep local file.
git rm --cached filename
```

---

## 17. Rename / Move

```bash
# Rename or move a tracked file.
git mv oldname newname
```

---

## 18. Remote Branches

```bash
# List remote branches.
git branch -r

# Create local branch tracking remote branch.
git switch --track origin/<branch>

# Show branch tracking information.
git branch -vv
```

---

## 19. Tags

```bash
# List tags.
git tag

# Create tag.
git tag v1.0.0

# Create annotated tag.
git tag -a v1.0.0 -m "Release 1.0.0"

# Push tag.
git push origin v1.0.0

# Push all tags.
git push origin --tags

# Delete local tag.
git tag -d v1.0.0
```

---

## 20. .gitignore

```bash
touch .gitignore
```

```text
__pycache__/
.venv/
.env
*.log
node_modules/
dist/
build/
```

> Files listed in `.gitignore` are not tracked.

---

## 21. Search History

```bash
# Show file history.
git log -- filename

# Show who changed each line.
git blame filename

# Find commits where text was added/removed.
git log -S "text"
```



---

## 22. Compare Branches

```bash
# Compare two branches.
git diff main..feature

# Commits in `feature` but not `main`.
git log main..feature
```

---

## 23. Rebase

```bash
git switch <branch>

# Move branch commits on top of latest `main`.
git rebase main

# Continue after resolving conflict.
git rebase --continue

# Cancel rebase.
git rebase --abort

# Interactively edit recent commits.
git rebase -i HEAD~3
```

> ⚠️ **Avoid rebasing shared/public commits unless you understand the impact.**

---

## 24. Cherry-Pick

```bash
# Apply one commit to the current branch.
git cherry-pick <commit>

# Cancel cherry-pick.
git cherry-pick --abort
```



---

## 25. Conflict Handling

### Resolve

```bash
git status

# Edit conflicted files

git add <resolved-file>

git commit
```

### During Rebase

```bash
git add <resolved-file>

git rebase --continue
```

### Cancel

```bash
git merge --abort

git rebase --abort
```

---

## 26. Clean Untracked Files

```bash
# Preview files that will be removed.
git clean -n

# Remove untracked files.
git clean -f

# Remove untracked files + directories.
git clean -fd
```



> ⚠️ **Use carefully — deleted files are not recoverable through Git.**

---

## 27. Git Reflog

```bash
# Find previous HEAD positions.
git reflog

# Recover from many accidental resets.
git reset --hard <reflog-commit>
```

---

## 28. Common Daily Workflow

```bash
git status

git switch main

git pull

git switch -c feature/my-feature

# Make changes

git status

git add .

git diff --staged

git commit -m "Add my feature"

git push -u origin feature/my-feature
```

---

## 29. Update Feature Branch

### Using Merge
```bash
git switch main
git pull

# Keep feature branch updated with `main`.
git switch feature/my-feature
git merge main
```

### Using Rebase
```bash
git switch main
git pull

git switch feature/my-feature
git rebase main
```

---

## 30. Quick Command Order

```text
1. git clone / git init
        ↓
2. git status
        ↓
3. git switch -c <branch>
        ↓
4. Make changes
        ↓
5. git status
        ↓
6. git add .
        ↓
7. git diff --staged
        ↓
8. git commit -m "message"
        ↓
9. git pull / git fetch
        ↓
10. git push
```

---

## 31. Most Used Commands

```bash
git status
git add .
git commit -m "message"
git push
git pull

git switch -c <branch>
git switch <branch>

git merge <branch>
git rebase <branch>

git stash
git stash pop

git log --oneline
git diff

git restore <file>
git restore --staged <file>

git reset
git revert <commit>

git remote -v
git fetch
```

> **Remember:**
> `add` → stage
> `commit` → save locally
> `push` → upload
> `pull` → download + integrate
> `fetch` → download only
> `merge` → combine branches
> `rebase` → move commits
> `stash` → temporarily store changes
> `revert` → safely undo a commit
