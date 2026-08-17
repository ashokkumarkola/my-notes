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
> Add all changes.
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
git pull
```

> Fetch + integrate remote changes.

```bash
git pull origin main
```

> Pull specific branch.

```bash
git pull --rebase
```

> Pull using rebase instead of merge.

---

## 12. Fetch

```bash
git fetch
```

> Download remote changes without merging.

```bash
git fetch origin
```

```bash
git fetch --all
```

> Fetch from all remotes.

---

## 13. Stash

```bash
git stash
```

> Temporarily save uncommitted changes.

```bash
git stash push -m "message"
```

> Save stash with a name.

```bash
git stash list
```

> List stashes.

```bash
git stash pop
```

> Apply latest stash + remove it.

```bash
git stash apply
```

> Apply latest stash without removing it.

```bash
git stash apply stash@{0}
```

> Apply specific stash.

```bash
git stash drop stash@{0}
```

> Delete specific stash.

```bash
git stash clear
```

> Delete all stashes.

---

## 14. Undo Changes

### Unstage File

```bash
git restore --staged filename
```

> Remove file from staging.

---

### Discard File Changes

```bash
git restore filename
```

> Discard uncommitted changes.

```bash
git restore .
```

> Discard all working-directory changes.

---

### Reset

```bash
git reset
```

> Unstage changes.

```bash
git reset --soft HEAD~1
```

> Undo commit, keep changes staged.

```bash
git reset --mixed HEAD~1
```

> Undo commit, keep changes unstaged.

```bash
git reset --hard HEAD~1
```

> Undo commit and discard changes.

> ⚠️ **Be careful with `--hard`.**

---

## 15. Revert

```bash
git revert <commit>
```

> Create a new commit that reverses another commit.

```bash
git revert HEAD
```

> Revert latest commit.

> **Reset** → changes history
> **Revert** → safely creates an opposite commit

---

## 16. Remove Files

```bash
git rm filename
```

> Delete file + stage deletion.

```bash
git rm -r folder/
```

> Delete folder + stage deletion.

```bash
git rm --cached filename
```

> Remove from Git but keep local file.

---

## 17. Rename / Move

```bash
git mv oldname newname
```

> Rename or move a tracked file.

---

## 18. Remote Branches

```bash
git branch -r
```

> List remote branches.

```bash
git switch --track origin/<branch>
```

> Create local branch tracking remote branch.

```bash
git branch -vv
```

> Show branch tracking information.

---

## 19. Tags

```bash
git tag
```

> List tags.

```bash
git tag v1.0.0
```

> Create tag.

```bash
git tag -a v1.0.0 -m "Release 1.0.0"
```

> Create annotated tag.

```bash
git push origin v1.0.0
```

> Push tag.

```bash
git push origin --tags
```

> Push all tags.

```bash
git tag -d v1.0.0
```

> Delete local tag.

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
git log -- filename
```

> Show file history.

```bash
git blame filename
```

> Show who changed each line.

```bash
git log -S "text"
```

> Find commits where text was added/removed.

---

## 22. Compare Branches

```bash
git diff main..feature
```

> Compare two branches.

```bash
git log main..feature
```

> Commits in `feature` but not `main`.

---

## 23. Rebase

```bash
git switch <branch>

git rebase main
```

> Move branch commits on top of latest `main`.

```bash
git rebase --continue
```

> Continue after resolving conflict.

```bash
git rebase --abort
```

> Cancel rebase.

```bash
git rebase -i HEAD~3
```

> Interactively edit recent commits.

> ⚠️ **Avoid rebasing shared/public commits unless you understand the impact.**

---

## 24. Cherry-Pick

```bash
git cherry-pick <commit>
```

> Apply one commit to the current branch.

```bash
git cherry-pick --abort
```

> Cancel cherry-pick.

---

## 25. Conflict Handling

```text
<<<<<<< HEAD
Current branch
=======
Incoming changes
>>>>>>> branch
```

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
```

```bash
git rebase --abort
```

---

## 26. Clean Untracked Files

```bash
git clean -n
```

> Preview files that will be removed.

```bash
git clean -f
```

> Remove untracked files.

```bash
git clean -fd
```

> Remove untracked files + directories.

> ⚠️ **Use carefully — deleted files are not recoverable through Git.**

---

## 27. Git Reflog

```bash
git reflog
```

> Find previous HEAD positions.

```bash
git reset --hard <reflog-commit>
```

> Recover from many accidental resets.

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

```bash
git switch main
git pull

git switch feature/my-feature
git merge main
```

> Keep feature branch updated with `main`.

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
