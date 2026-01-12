# Git Command Quick Reference Cheat Sheet


## Introduction

Git is a version control system that helps you track changes in your code. GitHub is a platform for hosting Git repositories online and collaborating with others.

### Why Use Git?
- Track changes in your code over time
- Collaborate with team members
- Back up your work to the cloud
- Revert to previous versions if something breaks
- Work on multiple features simultaneously

  
## Basic Concepts

### Repository (Repo)
A folder that Git tracks. Contains your project files and the `.git` folder with all version history.

### Commit
A snapshot of your project at a specific point in time. Like a save point in a video game.

### Branch
A separate line of development. Allows you to work on features without affecting the main code.

### Remote
A version of your repository hosted on GitHub (or another service).

### High level overview: Working Directory → Staging Area → Repository

```
  git status -> git add ->  git commit -> git push
```

---

[text](https://www.atlassian.com/git/tutorials/atlassian-git-cheatsheet)

## Basic Workflow with Github codespaces
1. Create repo in GitHub in the browser
<img width="657" height="158" alt="New repo" src="https://github.com/user-attachments/assets/76c3fe19-8f7f-4ef1-8a08-951b4fc8b368" />
<img width="1590" height="752" alt="Repo setup" src="https://github.com/user-attachments/assets/9149f0bc-d5c3-47ba-b522-c08a76e838aa" />

2. Launch Codespaces on the new repo
<img width="966" height="233" alt="Creating a codespace" src="https://github.com/user-attachments/assets/d6252168-ef59-4235-acea-7cbdb218bab8" />

3. Create a file such as README directly in the VSCode running on the Codespaces. 

Then start doing git commands!

```bash
# Check status. Files which have changed since last commit/push AND staged are in green.
git status (important)
git status -s                    # Short format

# 1) Add files to staging (important).
git add <file>                   # Add specific file
git add .                        # Add all changes
git add *.py                     # Add all Python files
git add --all                    # Add all (including deletions) (personal favourite JY)

# 2) Commit changes (important)
git commit -m "message"          # Commit with message. Make sure the message is clear and not keyboard spam for the sake of a message.
git commit -am "message"         # Add and commit tracked files
git commit --amend               # Modify last commit

# 3) Push changes (important)
git push                         # To tracking branch
git push --all                   # Push all branches
```

If you master the above, then you are 90% there in your git learning journey!
---

## Branches

```bash
# List branches
git branch                       # Local branches

# Create branch
git branch <name>                # Create branch
git checkout -b <name>           # Create and switch

# Switch branches
git checkout <branch>            # Switch to branch
git checkout -                   # Switch to previous branch

# Rename branch
git branch -m <old> <new>        # Rename branch

# Delete branch
git branch -d <branch>           # Delete (safe)
git branch -D <branch>           # Force delete
```

---

## Merging

```bash
# Merge branch into current
git merge <branch>

# Abort merge (if conflicts)
git merge --abort

# Continue after resolving conflicts
git add <resolved-files>
git commit
```

---

## Remote Repositories

```bash

# Pull changes (fetch + merge)
git pull                         # From tracking branch
git pull <remote> <branch>       # From specific branch
git pull --rebase                # Pull with rebase

```

---

## History & Logs

```bash
# View commit history
git log                          # Full history
git log --oneline                # Compact format
git log --graph                  # Show graph
git log --all                    # All branches
git log -n 5                     # Last 5 commits
git log --since="2 weeks ago"    # Recent commits
git log --author="Name"          # By author

# View specific commit
git show <commit>                # Show commit details
git show HEAD                    # Show last commit
git show HEAD~2                  # Show 2 commits back

# File history
git log <file>                   # Commits affecting file
git log -p <file>                # With diff
```

---

## Undoing Changes

```bash
# Discard working directory changes
git checkout -- <file>           # Discard changes
git restore <file>               # Modern syntax

# Unstage files
git reset <file>                 # Unstage file
git reset                        # Unstage all
git restore --staged <file>      # Modern syntax

# Undo commits
git reset --soft HEAD~1          # Undo commit, keep changes staged
git reset HEAD~1                 # Undo commit, unstage changes
git reset --hard HEAD~1          # Undo commit, discard changes (important)

# Revert commit (create new commit)
git revert <commit>              # Revert specific commit
git revert HEAD                  # Revert last commit
```

---

## Comparing

```bash
# Compare changes
git diff                         # Working vs staging
git diff --staged                # Staging vs repository
git diff HEAD                    # Working vs repository
git diff <branch1> <branch2>     # Between branches
git diff <commit1> <commit2>     # Between commits
```

---

## Common Scenarios

### Start new project
```bash
git status
[add new python file hello.py with code]
git status
git add hello.py
git commit -m "Initial commit"
git push
```

### Fix merge conflict
```bash
git pull origin main
# CONFLICT appears
# Edit conflicted files
git add <resolved-files>
git commit -m "Resolve merge conflict"
git push origin main
```

### Undo last commit (not pushed)
```bash
git reset --soft HEAD~1
# Make corrections
git add .
git commit -m "Corrected commit"
```

---

**Online Resources:**
- Official Git Docs: https://git-scm.com/doc
- GitHub Docs: https://docs.github.com
- Git Cheat Sheet: https://education.github.com/git-cheat-sheet-education.pdf

---

## Pro Tips

1. **Commit early, commit often** - Small, logical commits are better
2. **Write good messages** - Future you will thank present you.
   
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

3. **Pull before push** - Avoid conflicts
4. **Use branches** - Keep main stable
5. **Review before commit** - Use `git status`
6. **Read error messages** - Git is usually helpful

---

## Common Patterns

```bash
# Start work session
git pull origin main
git checkout -b feature/my-feature

# During work
git status                       # Check often
git diff                         # Review changes
git add <files>
git commit -m "message"

# End work session
git push -u origin feature/my-feature

# After PR approved
git checkout main
git pull origin main
git branch -d feature/my-feature
```

---

**Print this and keep it at your desk!** 📋

Extra:


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

