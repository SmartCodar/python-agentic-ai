# 🧠 Git Essentials – Beginner to Pro (with SSH & Multi-Repo Setup)

This article will guide you through setting up Git on Windows and Ubuntu EC2, configuring SSH keys for GitHub, cloning a private repository, resolving merge conflicts, and using Git effectively — especially when working with multiple projects or repositories.

---

## 🔧 Step 1: Install Git

### 📦 On Ubuntu EC2
```bash
# Option 1: Standard Git installation
sudo apt update
sudo apt install git -y

# Option 2: Latest Git from PPA
sudo add-apt-repository ppa:git-core/ppa -y
sudo apt update && sudo apt install git -y
```
✅ *This installs Git on your Linux EC2 instance so you can manage code repositories from the terminal.*

### 🖥️ On Windows

1. Download Git for Windows:  
   👉 https://git-scm.com/download/win  
2. During installation:
   - Choose "Git from the command line and also from 3rd-party software"
   - Keep line endings as "Checkout Windows-style, commit Unix-style"
   - Enable Git Credential Manager (optional)

3. Verify installation:
```bash
git --version
```

---

## 🔐 Step 2: Generate SSH Key (Multi-Repo Friendly)

To avoid key collisions when managing multiple GitHub accounts or projects:

```bash
# Generate a named SSH key
ssh-keygen -t rsa -b 4096 -f ~/.ssh/chocosoft_ai -C "ameet@chocosoft.in"
```

Follow the prompts. Do **not** overwrite existing keys unless you're resetting access.

---

## 🚀 Step 3: Add SSH Key to Agent and GitHub

Start SSH agent and add your custom key:

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/chocosoft_ai
```

Copy the public key:

```bash
cat ~/.ssh/chocosoft_ai.pub
```

Then:
1. Go to GitHub > Settings > SSH and GPG Keys
2. Click “New SSH Key”, name it something like `EC2-Zennial`
3. Paste the copied key and save

✅ *You can now connect to GitHub without entering credentials every time.*

---

## 🌐 Step 4: SSH Config (Multiple Key Management)

If you use multiple SSH keys across repos:

```bash
nano ~/.ssh/config
```

Paste:

```text
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/chocosoft_ai
```

✅ *This ensures Git uses the correct identity file when cloning or pushing.*

---

## 📥 Step 5: Clone the Repository (SSH)

Use the SSH URL to securely clone the private repository:

```bash
git clone git@github.com:Zennial-Pro/fullstack-agentic-ai.git
```

This will create a directory `fullstack-agentic-ai` with the project code.

---

## 🔄 Step 6: Most Common Git Commands (With Descriptions)

### ✅ Check Current Status
```bash
git status
```
Displays modified, untracked, or staged files.

### 📂 Initialize Git in a Directory
```bash
git init
```
Sets up a new Git repository in your current folder.

### 💾 Add Files to Staging
```bash
git add .
```
Stages all changed files for the next commit.

### 📦 Commit Changes
```bash
git commit -m "Initial commit with project structure"
```
Saves a snapshot of staged files.

### 🚀 Push Changes to GitHub
```bash
git push origin main
```
Uploads your commits to the main branch on GitHub.

### 🔄 Pull Latest Code
```bash
git pull origin main
```
Downloads and merges updates from the remote repo.

### 🌿 Create and Switch to New Branch
```bash
git checkout -b feature/pdf-generation
```
Creates and switches to a new branch for isolated development.

### 🔁 Switch Branch
```bash
git checkout main
```
Changes to another existing branch.

### 🔀 Merge Branch
```bash
git merge feature/pdf-generation
```
Combines a feature branch into your current one.

### 🔁 Undo Last Commit (Keep Changes)
```bash
git reset --soft HEAD~1
```

### 🧼 Remove File from Git
```bash
git rm --cached .env
```

### 🧹 Remove File From Git and Disk
```bash
git rm file.txt
```

### 🔍 See Changes (Uncommitted)
```bash
git diff
```

### 📜 Commit History
```bash
git log --oneline --graph
```

### 🛠️ Set Git Identity
```bash
git config --global user.name "AI Developer"
git config --global user.email "ameet@chocosoft.in"
```

### 🔗 Check GitHub Remote URL
```bash
git remote -v
```

### 🧠 Shortcut to Commit Staged Files
```bash
git commit -am "Quick patch"
```

### ⚠️ Hard Reset (Dangerous!)
```bash
git reset --hard
```

---

## ✅ DOs and ❌ DON’Ts

### ✅ DOs
- Use clear, consistent commit messages.
- Work in branches for every feature or fix.
- Pull frequently to reduce conflict chances.
- Use `.gitignore` to skip sensitive files.

### ❌ DON’Ts
- Don’t commit to `main` without testing.
- Don’t push large files or secrets.
- Don’t ignore conflict warnings.
- Don’t force push unless absolutely needed.

---

## 🔧 How to Resolve Merge Conflicts

1. Git will mark conflict areas like:
```text
<<<<<<< HEAD
Your local changes
=======
Their remote changes
>>>>>>> branch-name
```

2. Manually edit the file to keep the correct changes.

3. Mark resolved by staging the file:
```bash
git add conflicted_file.py
```

4. Finalize with a commit:
```bash
git commit -m "Resolved conflict in conflicted_file.py"
```

---

## 🧪 Git Knowledge Check – 20 Questions

| # | Question |
|--:|:---------|
| 1 | What does `git init` do? |
| 2 | What’s the difference between `git add` and `git commit`? |
| 3 | Why use SSH over HTTPS for GitHub? |
| 4 | How do you check which branch you’re on? |
| 5 | What does `git status` show you? |
| 6 | What happens when you clone a repository? |
| 7 | How do you safely switch between branches? |
| 8 | What’s the use of `.gitignore`? |
| 9 | How do you undo your last commit? |
| 10 | How do you resolve a merge conflict? |
| 11 | What is the difference between `origin` and `upstream`? |
| 12 | How can you view your commit history? |
| 13 | What does `git fetch` do vs `git pull`? |
| 14 | How do you remove a file from Git tracking but not delete it? |
| 15 | What is the HEAD in Git? |
| 16 | How do you create a new branch and push it to GitHub? |
| 17 | Why is commit message quality important? |
| 18 | How do you revert a commit that has already been pushed? |
| 19 | How can you find out who wrote a particular line of code? |
| 20 | What does `git stash` do and when would you use it? |

---
