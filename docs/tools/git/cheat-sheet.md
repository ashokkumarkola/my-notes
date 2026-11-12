# Git Cheat Sheet

Full reference: [Commands](git-commands.md).

## Flow

```text
Working dir --add--> Staging --commit--> Local repo --push--> Remote
            <--restore--        <--reset--          <--pull/fetch--
```

## Setup

```bash
git config --global user.name "Name"
git config --global user.email "me@example.com"
git config --global init.defaultBranch main
git config --list
```

## Start

```bash
git init
git clone <url>
git clone <url> folder
```

## Daily

```bash
git status
git add file | git add .
git commit -m "msg"
git commit -am "msg"            # tracked files only
git push
git pull                        # fetch + merge
git log --oneline --graph -10
git diff                        # unstaged
git diff --staged               # staged
```

## Branches

```bash
git branch                      # list
git switch -c feature           # create + switch
git switch main
git merge feature
git branch -d feature           # delete merged
git push -u origin feature      # first push, set upstream
git push origin --delete feature
```

## Remote

```bash
git remote -v
git remote add origin <url>
git remote set-url origin <url>
git fetch
```

## Undo

| Situation | Command |
|---|---|
| Discard file changes | `git restore file` |
| Unstage file | `git restore --staged file` |
| Fix last commit msg | `git commit --amend -m "new"` |
| Undo last commit, keep changes | `git reset --soft HEAD~1` |
| Undo last commit, drop changes | `git reset --hard HEAD~1` |
| Undo pushed commit (safe) | `git revert <hash>` |
| Find lost commit | `git reflog` |

`reset --hard` deletes uncommitted work. No undo.

## Stash

```bash
git stash push -u -m "wip"
git stash list
git stash pop
git stash drop
```

## Tags

```bash
git tag -a v1.0 -m "release"
git push origin v1.0
git tag
```

## Rename / move

```bash
git mv old.md new.md            # keeps history
git log --follow new.md
```
