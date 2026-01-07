# Git Command Quick Reference Cheat Sheet

[text](https://www.atlassian.com/git/tutorials/atlassian-git-cheatsheet)

---

## Creating Repositories

```bash
# Initialize new repo
git init

# Clone existing repo
git clone <url>

# Clone specific branch
git clone -b <branch> <url>
```

---

## Basic Workflow

```bash
# Check status
git status
git status -s                    # Short format

# Add files to staging
git add <file>                   # Add specific file
git add .                        # Add all changes
git add *.py                     # Add all Python files
git add --all                    # Add all (including deletions)

# Commit changes
git commit -m "message"          # Commit with message
git commit -am "message"         # Add and commit tracked files
git commit --amend               # Modify last commit

# View changes
git diff                         # Unstaged changes
git diff --staged                # Staged changes
git diff <file>                  # Changes in specific file
```

---

## Branches

```bash
# List branches
git branch                       # Local branches
git branch -a                    # All branches (local + remote)
git branch -r                    # Remote branches

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

# Push changes
git push                         # To tracking branch
git push <remote> <branch>       # To specific branch
git push -u <remote> <branch>    # Set upstream and push
git push --all                   # Push all branches
git push --tags                  # Push all tags
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
git reset --hard HEAD~1          # Undo commit, discard changes

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
git init
git add .
git commit -m "Initial commit"
git remote add origin <url>
git push -u origin main
```

### Clone and contribute
```bash
git clone <url>
cd <repo>
git checkout -b feature-branch
# Make changes
git add .
git commit -m "Add feature"
git push -u origin feature-branch
# Create Pull Request on GitHub
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
2. **Write good messages** - Future you will thank present you
3. **Pull before push** - Avoid conflicts
4. **Use branches** - Keep main stable
5. **Review before commit** - Use `git diff` and `git status`
6. **Never commit secrets** - Use .gitignore
7. **Read error messages** - Git is usually helpful
8. **Practice daily** - Best way to learn

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
