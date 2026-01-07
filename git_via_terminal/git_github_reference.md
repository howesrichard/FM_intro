# Git and GitHub Terminal Guide for FINMA Students

## Table of Contents
1. [Introduction](#introduction)
2. [Setup](#setup)
3. [Basic Concepts](#basic-concepts)
4. [Essential Commands](#essential-commands)
5. [Common Workflows](#common-workflows)
6. [Best Practices](#best-practices)
7. [Troubleshooting](#troubleshooting)

---

## Introduction

Git is a version control system that helps you track changes in your code. GitHub is a platform for hosting Git repositories online and collaborating with others.

### Why Use Git?
- Track changes in your code over time
- Collaborate with team members
- Back up your work to the cloud
- Revert to previous versions if something breaks
- Work on multiple features simultaneously

---

## Setup

### First-Time Configuration

Before using Git, configure your identity:

```bash
# Set your name (use your real name)
git config --global user.name "Your Name"

# Set your email (use your GitHub email)
git config --global user.email "your.email@example.com"

# Check your configuration
git config --list
```

### Verify Installation

```bash
# Check Git version
git --version

# Should show something like: git version 2.x.x
```

---

## Basic Concepts

### Repository (Repo)
A folder that Git tracks. Contains your project files and the `.git` folder with all version history.

### Commit
A snapshot of your project at a specific point in time. Like a save point in a video game.

### Branch
A separate line of development. Allows you to work on features without affecting the main code.

### Remote
A version of your repository hosted on GitHub (or another service).

### Working Directory → Staging Area → Repository

```
Working Directory  →  Staging Area  →  Local Repository  →  Remote Repository
   (git add)           (git commit)          (git push)
```

---

## Essential Commands

### 1. Creating and Cloning Repositories

#### Initialize a New Repository
```bash
# Create a new Git repository in the current folder
git init

# Creates a hidden .git folder
```

#### Clone an Existing Repository
```bash
# Clone a repository from GitHub
git clone https://github.com/username/repository-name.git

# Clone to a specific folder name
git clone https://github.com/username/repository-name.git my-folder

# Clone a specific branch
git clone -b branch-name https://github.com/username/repository-name.git
```

**Example:**
```bash
# Clone your Python labs repository
git clone https://github.com/yourusername/finma-python-labs.git
cd finma-python-labs
```

---

### 2. Checking Status

#### View Repository Status
```bash
# Show which files have been modified, staged, or are untracked
git status

# Short status format
git status -s
```

**Output explanation:**
```
On branch main
Changes not staged for commit:
  modified:   lab01.ipynb        # Modified but not staged
  
Untracked files:
  lab02.ipynb                    # New file, not tracked yet
```

---

### 3. Adding Files (Staging)

#### Add Specific Files
```bash
# Add a single file
git add filename.py

# Add multiple specific files
git add file1.py file2.py file3.py

# Add all Python files
git add *.py

# Add all files in a directory
git add notebooks/
```

#### Add All Changes
```bash
# Add all modified and new files
git add .

# Alternative (more explicit)
git add --all

# Add all files (including deletions)
git add -A
```

**Example workflow:**
```bash
# Check what needs to be added
git status

# Add specific lab file
git add lab05.ipynb

# Add all solution files
git add *_solutions.ipynb

# Add everything
git add .
```

---

### 4. Committing Changes

#### Create a Commit
```bash
# Commit staged changes with a message
git commit -m "Your descriptive message"

# Commit with a longer message (opens editor)
git commit

# Add and commit in one step (only for tracked files)
git commit -am "Your message"
```

**Good commit messages:**
```bash
git commit -m "Add Lab 5 on lists and dictionaries"
git commit -m "Fix bug in portfolio calculation function"
git commit -m "Update README with installation instructions"
git commit -m "Complete exercises 1-4 in Lab 7"
```

**Bad commit messages:**
```bash
git commit -m "stuff"          # Too vague
git commit -m "asdfgh"         # Meaningless
git commit -m "changes"        # Not descriptive
```

---

### 5. Viewing History

#### View Commit History
```bash
# Show commit history
git log

# Show compact one-line format
git log --oneline

# Show last N commits
git log -n 5

# Show commits with file changes
git log --stat

# Show commits as a graph
git log --graph --oneline --all
```

**Example output:**
```
commit 3a5f7b2 (HEAD -> main, origin/main)
Author: Student Name <student@example.com>
Date:   Mon Jan 4 10:30:00 2026

    Complete Lab 7 file I/O exercises

commit 8d4c1a9
Author: Student Name <student@example.com>
Date:   Sun Jan 3 15:20:00 2026

    Add Lab 6 functions exercises
```

---

### 6. Working with Branches

#### View Branches
```bash
# List all local branches
git branch

# List all branches (including remote)
git branch -a

# Show current branch
git branch --show-current
```

#### Create Branches
```bash
# Create a new branch
git branch feature-name

# Create and switch to new branch
git checkout -b feature-name

# Modern syntax (Git 2.23+)
git switch -c feature-name
```

#### Switch Branches
```bash
# Switch to existing branch
git checkout branch-name

# Modern syntax (Git 2.23+)
git switch branch-name

# Switch to previous branch
git checkout -
```

#### Delete Branches
```bash
# Delete a local branch (if merged)
git branch -d branch-name

# Force delete a branch (even if not merged)
git branch -D branch-name

# Delete a remote branch
git push origin --delete branch-name
```

**Example workflow:**
```bash
# Create a branch for Lab 8
git checkout -b lab08-development

# Work on your lab...
git add lab08.ipynb
git commit -m "Complete Lab 8 exercises"

# Switch back to main
git checkout main

# Merge your changes
git merge lab08-development
```

---

### 7. Working with Remote Repositories

#### View Remotes
```bash
# List remote repositories
git remote

# List with URLs
git remote -v

# Show remote details
git remote show origin
```

#### Add a Remote
```bash
# Add a remote repository
git remote add origin https://github.com/username/repo.git

# Add a remote with a custom name
git remote add upstream https://github.com/original/repo.git
```

#### Pull Changes (Download)
```bash
# Pull changes from remote
git pull

# Pull from specific remote and branch
git pull origin main

# Pull with rebase (cleaner history)
git pull --rebase
```

#### Push Changes (Upload)
```bash
# Push to remote
git push

# Push to specific remote and branch
git push origin main

# Push a new branch
git push -u origin feature-name

# Force push (use with caution!)
git push --force
```

**Example workflow:**
```bash
# Get latest changes from GitHub
git pull origin main

# Make your changes
git add lab06.ipynb
git commit -m "Complete Lab 6 functions"

# Upload your changes to GitHub
git push origin main
```

---

### 8. Comparing Changes

#### View Differences
```bash
# Show unstaged changes
git diff

# Show staged changes
git diff --staged

# Show changes in a specific file
git diff filename.py

# Compare two branches
git diff branch1..branch2

# Compare two commits
git diff commit1 commit2
```

---

### 9. Undoing Changes

#### Unstage Files
```bash
# Unstage a file (keep changes)
git reset filename.py

# Unstage all files
git reset
```

#### Discard Changes
```bash
# Discard changes in a file (WARNING: Cannot undo!)
git checkout -- filename.py

# Discard all changes (WARNING: Cannot undo!)
git checkout -- .

# Modern syntax
git restore filename.py
```

#### Undo Last Commit
```bash
# Undo commit but keep changes staged
git reset --soft HEAD~1

# Undo commit and unstage changes
git reset HEAD~1

# Undo commit and discard changes (WARNING!)
git reset --hard HEAD~1
```

---

## Common Workflows

### Workflow 1: Starting a New Project

```bash
# On GitHub: Create a new repository

# Clone it to your computer
git clone https://github.com/yourusername/finma-python-labs.git
cd finma-python-labs

# Create a README
echo "# FINMA Python Labs" > README.md

# Add and commit
git add README.md
git commit -m "Initial commit with README"

# Push to GitHub
git push origin main
```

---

### Workflow 2: Daily Work Routine

```bash
# Start your day - get latest changes
git pull origin main

# Create a new branch for today's work
git checkout -b lab07-solutions

# Work on your code...
# ... make changes to files ...

# Check what changed
git status
git diff

# Stage your changes
git add lab07_solutions.ipynb

# Commit with a good message
git commit -m "Complete Lab 7 exercises 1-5"

# Continue working...
git add lab07_solutions.ipynb
git commit -m "Complete Lab 7 exercises 6-8"

# Push your branch to GitHub
git push -u origin lab07-solutions

# Switch back to main
git checkout main

# Merge your work
git merge lab07-solutions

# Push to main
git push origin main
```

---

### Workflow 3: Collaborating on a Group Project

```bash
# Clone the team repository
git clone https://github.com/team/project.git
cd project

# Create your feature branch
git checkout -b feature/portfolio-analysis

# Make your changes
git add portfolio_analysis.py
git commit -m "Add portfolio analysis module"

# Get latest changes from team
git checkout main
git pull origin main

# Merge main into your branch
git checkout feature/portfolio-analysis
git merge main

# Resolve any conflicts...

# Push your feature branch
git push -u origin feature/portfolio-analysis

# On GitHub: Create a Pull Request

# After PR is approved and merged
git checkout main
git pull origin main
git branch -d feature/portfolio-analysis
```

---

### Workflow 4: Fixing a Mistake

```bash
# Made changes but haven't committed yet
git status
git checkout -- filename.py    # Discard changes

# Committed but didn't push yet
git reset --soft HEAD~1         # Undo commit, keep changes
# Fix your code
git add .
git commit -m "Corrected commit"

# Already pushed to GitHub (careful!)
git revert HEAD                 # Create new commit that undoes last commit
git push origin main
```

---

## Best Practices

### 1. Commit Often
- Make small, logical commits
- Each commit should represent one change or feature
- Don't wait until end of day to commit everything

### 2. Write Good Commit Messages
```bash
# Good
git commit -m "Add input validation to calculate_return function"
git commit -m "Fix divide by zero error in portfolio analysis"
git commit -m "Update README with installation instructions"

# Bad
git commit -m "fixed stuff"
git commit -m "update"
git commit -m "asdf"
```

### 3. Pull Before Push
```bash
# Always get latest changes first
git pull origin main

# Then push your changes
git push origin main
```

### 4. Use Branches for Features
```bash
# Don't work directly on main
git checkout -b feature/new-analysis

# Do your work
git add .
git commit -m "Add new analysis feature"

# Merge when ready
git checkout main
git merge feature/new-analysis
```

### 5. Don't Commit Sensitive Data
- Never commit passwords, API keys, or credentials
- Use `.gitignore` for sensitive files
- Use environment variables for secrets

### 6. Keep Your Repository Clean
```bash
# Use .gitignore for:
# - __pycache__/
# - .ipynb_checkpoints/
# - .env
# - *.pyc
# - venv/
```

---


## Troubleshooting

### Problem: Merge Conflicts

When Git can't automatically merge changes:

```bash
# You'll see something like:
Auto-merging lab05.ipynb
CONFLICT (content): Merge conflict in lab05.ipynb

# Open the file and look for:
Your changes

# Fix the conflict by choosing which code to keep
# Remove the conflict markers
# Then:
git add lab05.ipynb
git commit -m "Resolve merge conflict in lab05"
```

### Problem: Accidentally Committed to Wrong Branch

```bash
# If you haven't pushed yet:
git log --oneline    # Note the commit hash

git checkout correct-branch
git cherry-pick <commit-hash>

git checkout wrong-branch
git reset --hard HEAD~1
```

### Problem: Need to Undo a Push

```bash
# If you pushed something wrong (use with caution!)
git revert HEAD
git push origin main

# Or if no one else has pulled yet (dangerous!):
git reset --hard HEAD~1
git push --force origin main
```

### Problem: Forgot to Pull Before Making Changes

```bash
# You have local changes and remote has new commits
git pull origin main   # Get remote changes
git stash pop          # Reapply your changes
# Resolve any conflicts
git add .
git commit -m "Your message"
git push origin main
```

---

## Quick Reference Cheat Sheet

```bash
# Setup
git config --global user.name "Your Name"
git config --global user.email "your@email.com"

# Create
git init                                    # Initialize repository
git clone <url>                             # Clone repository

# Status
git status                                  # Check status
git log                                     # View history
git diff                                    # View changes

# Add & Commit
git add <file>                              # Stage file
git add .                                   # Stage all changes
git commit -m "message"                     # Commit changes

# Branch
git branch                                  # List branches
git branch <name>                           # Create branch
git checkout <name>                         # Switch branch
git checkout -b <name>                      # Create and switch
git merge <branch>                          # Merge branch

# Remote
git remote -v                               # List remotes
git pull                                    # Get remote changes
git push                                    # Send local changes
git push -u origin <branch>                 # Push new branch

# Undo
git reset <file>                            # Unstage file
git checkout -- <file>                      # Discard changes
git reset --soft HEAD~1                     # Undo last commit
```

---

## Additional Resources

### Learning More
- **GitHub Docs**: https://docs.github.com
- **Git Book**: https://git-scm.com/book/en/v2
- **GitHub Learning Lab**: https://lab.github.com

### GitHub Desktop (GUI Alternative)
If you prefer a graphical interface:
- Download: https://desktop.github.com
- Easier for beginners
- Good for visualizing branches and commits

### VS Code Integration
If using VS Code:
- Built-in Git support
- Source Control panel on left sidebar
- GitLens extension for advanced features

---

## Summary

**Remember the basic workflow:**

1. `git pull` - Get latest changes
2. Make your changes
3. `git status` - See what changed
4. `git add .` - Stage changes
5. `git commit -m "message"` - Commit changes
6. `git push` - Upload to GitHub

**Golden Rules:**
- Commit often with clear messages
- Pull before you push
- Use branches for new features
- Don't commit sensitive data
- When in doubt, check `git status`

Good luck with your version control journey! 🚀
