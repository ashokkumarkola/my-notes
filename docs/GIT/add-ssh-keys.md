# Git — Work + Personal Accounts on Ubuntu

## Goal

Use **two Git accounts** on the same Ubuntu system:

* **Work** → work GitHub account
* **Personal** → personal GitHub account

Each account uses a different SSH key.

---

## 1. Check SSH folder

```bash
ls -la ~/.ssh/
```

---

## 2. Create personal SSH key

```bash
ssh-keygen -t ed25519 -C "your-personal-email@example.com"
```

When asked where to save:

```text
/home/ashokkumar/.ssh/id_ed25519_personal
```

Do **not** overwrite the existing work key.

---

## 3. Start SSH agent

```bash
eval "$(ssh-agent -s)"
```

Add personal key:

```bash
ssh-add ~/.ssh/id_ed25519_personal
```

Check:

```bash
ssh-add -l
```

---

## 4. Copy personal public key

```bash
cat ~/.ssh/id_ed25519_personal.pub
```

Copy the complete output.

Add it to:

**GitHub → Settings → SSH and GPG keys → New SSH key**

---

## 5. Configure SSH

Open:

```bash
nano ~/.ssh/config
```

Example:

```ssh
# Work GitHub
Host github-work
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_work
    IdentitiesOnly yes

# Personal GitHub
Host github-personal
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_personal
    IdentitiesOnly yes
```

> Replace `id_ed25519_work` with the actual filename of your existing work key.

Save:

```text
Ctrl + O
Enter
Ctrl + X
```

---

## 6. Test personal GitHub

```bash
ssh -T git@github-personal
```

Expected:

```text
Hi YOUR_USERNAME! You've successfully authenticated,
but GitHub does not provide shell access.
```

---

# Personal Repository Setup

Go to your personal project:

```bash
cd ~/Documents/ASHOKA/LEARN/my-notes
```

Initialize Git:

```bash
git init
```

Use `main`:

```bash
git branch -M main
```

---

## 7. Set personal Git identity

This controls who appears as the author of your commits.

```bash
git config user.name "Your Personal Name"
git config user.email "your-personal-email@example.com"
```

Check:

```bash
git config user.name
git config user.email
```

---

## 8. Create GitHub repository

Create a repository on your personal GitHub account.

Example:

```text
my-notes
```

Don't initialize it with README if the local project already contains files.

---

## 9. Add personal remote

Use the **personal SSH alias**:

```bash
git remote add origin git@github-personal:YOUR_USERNAME/my-notes.git
```

Check:

```bash
git remote -v
```

Expected:

```text
origin  git@github-personal:YOUR_USERNAME/my-notes.git (fetch)
origin  git@github-personal:YOUR_USERNAME/my-notes.git (push)
```

---

## 10. First push

```bash
git add .
```

```bash
git commit -m "Initial commit"
```

```bash
git push -u origin main
```

---

# Daily Personal Workflow

After making changes:

```bash
git status
git add .
git commit -m "Update notes"
git push
```

---

# Work Repository

Your work repository should use the **work SSH alias**:

```bash
git@github-work:COMPANY/PROJECT.git
```

Example:

```bash
git clone git@github-work:company/project.git
```

Your personal repository uses:

```bash
git@github-personal:YOUR_USERNAME/my-notes.git
```

---

# Important Difference

There are **two separate things**:

### SSH key

Controls **which GitHub account you authenticate as**.

```text
SSH key
   ↓
GitHub account
```

### Git user.name / user.email

Controls **who is shown as the commit author**.

```text
git config
   ↓
Commit author
```

So for personal repositories:

```bash
git config user.name "Personal Name"
git config user.email "personal@example.com"
```

For work repositories:

```bash
git config user.name "Work Name"
git config user.email "work@company.com"
```

Because these are configured **inside each repository**, they won't collide.

---

# Useful Commands

Check remote:

```bash
git remote -v
```

Check current Git identity:

```bash
git config user.name
git config user.email
```

Check SSH keys loaded:

```bash
ssh-add -l
```

Test personal account:

```bash
ssh -T git@github-personal
```

Test work account:

```bash
ssh -T git@github-work
```

Check SSH configuration:

```bash
cat ~/.ssh/config
```

List SSH files:

```bash
ls -la ~/.ssh/
```

---

# Final Structure

```text
Ubuntu
│
├── Work
│   ├── Work GitHub account
│   ├── Work SSH key
│   └── git@github-work
│
└── Personal
    ├── Personal GitHub account
    ├── Personal SSH key
    └── git@github-personal
```

**Key idea:** Git doesn't get confused because the SSH `Host` aliases tell it which key to use.
