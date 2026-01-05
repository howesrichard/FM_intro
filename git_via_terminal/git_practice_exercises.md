# Git and GitHub Practice Exercises

## Overview

These hands-on exercises will help you practice essential Git and GitHub commands. Complete them in order, as later exercises build on earlier ones.

**Time required:** 2-3 hours  
**Prerequisites:** Git installed, GitHub account created

---

## Exercise 1: Initial Setup and Configuration

### Objective
Configure Git with your identity and verify the setup.

### Tasks

1. Set your name in Git:
```bash
git config --global user.name "Your Full Name"
```

2. Set your email (use your GitHub email):
```bash
git config --global user.email "your.email@example.com"
```

3. Verify your configuration:
```bash
git config --list
```

4. Check your Git version:
```bash
git --version
```

### Expected Output
You should see your name and email listed, and Git version should be 2.x or higher.

---

## Exercise 2: Creating Your First Repository

### Objective
Create a local Git repository and make your first commit.

### Tasks

1. Create a new folder for your project:
```bash
mkdir finma-git-practice
cd finma-git-practice
```

2. Initialize a Git repository:
```bash
git init
```

3. Check the status:
```bash
git status
```

4. Create a README file:
```bash
echo "# FINMA Git Practice" > README.md
```

5. Check status again:
```bash
git status
```

6. Add the README to staging:
```bash
git add README.md
```

7. Check status once more:
```bash
git status
```

8. Commit the file:
```bash
git commit -m "Initial commit: Add README"
```

9. View the commit history:
```bash
git log
```

### Questions to Answer
- What does "untracked file" mean?
- What is the difference between the working directory and the staging area?
- What information is shown in the git log output?

---

## Exercise 3: Making Multiple Commits

### Objective
Practice the add-commit workflow with multiple files.

### Tasks

1. Create a Python file:
```bash
code hello.py
```

2. 
```python
print('Hello, Git!')
```

3. Check status:
```bash
git status
```

4. Add both files:
```bash
git add hello.py .gitignore
```

5. Commit:
```bash
git commit -m "Add hello.py and gitignore"
```

6. Modify hello.py:
```bash
echo "print('Goodbye, Git!')" >> hello.py
```

7. Check the difference:
```bash
git diff hello.py
```

8. Add and commit the change:
```bash
git add hello.py
git commit -m "Add goodbye message to hello.py"
```

9. View the commit history:
```bash
git log --oneline
```

### Questions to Answer
- How does `git diff` help you?
- What does `--oneline` do to the log output?
- Why is .gitignore important?

---

## Exercise 4: Connecting to GitHub

### Objective
Create a GitHub repository and push your local repository to it.

### Tasks

1. **On GitHub.com:**
   - Click the "+" icon → "New repository"
   - Name it: `finma-git-practice`
   - Description: "Learning Git and GitHub"
   - Keep it public
   - Do NOT initialize with README (we already have one)
   - Click "Create repository"

2. **In your terminal:**

   Copy the repository URL from GitHub, then:

```bash
git remote add origin https://github.com/YOUR-USERNAME/finma-git-practice.git
```

3. Verify the remote:
```bash
git remote -v
```

4. Push your commits to GitHub:
```bash
git push -u origin main
```
   (If you get an error about 'master' vs 'main', use the branch name Git tells you)

5. **On GitHub.com:**
   - Refresh the page
   - Verify your files are there

### Questions to Answer
- What does "origin" refer to?
- What does the `-u` flag do in `git push -u`?
- Can you see your commit history on GitHub?

---

## Exercise 5: Pull, Modify, Push Workflow

### Objective
Practice the standard workflow for working with a remote repository.

### Tasks

1. **On GitHub.com:**
   - Navigate to your repository
   - Click on README.md
   - Click the pencil icon (Edit)
   - Add a line: "Edited on GitHub!"
   - Commit changes (use the GitHub interface)

2. **In your terminal:**

```bash
# Get the latest changes
git pull origin main

# View the updated README
cat README.md

# Create a new file
echo "def calculate_return(initial, final):" > portfolio.py
echo "    return ((final - initial) / initial) * 100" >> portfolio.py

# Add and commit
git add portfolio.py
git commit -m "Add portfolio return calculator"

# Push to GitHub
git push origin main
```

3. **On GitHub.com:**
   - Refresh and verify portfolio.py is there

### Questions to Answer
- What happens if you forget to `git pull` before making changes?
- How does Git handle conflicts between local and remote changes?

---

## Exercise 6: Working with Branches

### Objective
Learn to create and work with branches.

### Tasks

1. Check current branch:
```bash
git branch
```

2. Create a new branch:
```bash
git checkout -b feature/risk-calculator
```

3. Verify you're on the new branch:
```bash
git branch
```

4. Create a new file on this branch:
```bash
cat > risk_calculator.py << EOF
def calculate_volatility(prices):
    """Calculate volatility of price series"""
    import statistics
    returns = []
    for i in range(1, len(prices)):
        ret = (prices[i] - prices[i-1]) / prices[i-1]
        returns.append(ret)
    return statistics.stdev(returns)
EOF
```

5. Add and commit:
```bash
git add risk_calculator.py
git commit -m "Add volatility calculator function"
```

6. Push the new branch to GitHub:
```bash
git push -u origin feature/risk-calculator
```

7. Switch back to main:
```bash
git checkout main
```

8. Verify the file isn't there:
```bash
ls risk_calculator.py
```
   (Should say "No such file")

9. Switch back to your branch:
```bash
git checkout feature/risk-calculator
```

10. Verify the file is back:
```bash
ls risk_calculator.py
```

### Questions to Answer
- Why use branches instead of working directly on main?
- What happens to your files when you switch branches?
- How can you see all branches, including remote ones?

---

## Exercise 7: Merging Branches

### Objective
Practice merging a feature branch back into main.

### Tasks

1. Make sure you're on the feature branch:
```bash
git checkout feature/risk-calculator
```

2. Add another function to risk_calculator.py:
```bash
cat >> risk_calculator.py << EOF

def calculate_sharpe_ratio(returns, risk_free_rate=0.02):
    """Calculate Sharpe ratio"""
    import statistics
    avg_return = statistics.mean(returns)
    volatility = statistics.stdev(returns)
    return (avg_return - risk_free_rate) / volatility
EOF
```

3. Add and commit:
```bash
git add risk_calculator.py
git commit -m "Add Sharpe ratio calculator"
```

4. Push to GitHub:
```bash
git push origin feature/risk-calculator
```

5. Switch to main branch:
```bash
git checkout main
```

6. Merge your feature branch:
```bash
git merge feature/risk-calculator
```

7. Push main to GitHub:
```bash
git push origin main
```

8. View the commit history:
```bash
git log --oneline --graph --all
```

9. Delete the feature branch (it's now merged):
```bash
git branch -d feature/risk-calculator
```

10. Delete it from GitHub too:
```bash
git push origin --delete feature/risk-calculator
```

### Questions to Answer
- What does "fast-forward merge" mean?
- When might you see a merge conflict?
- Why delete branches after merging?

---

## Exercise 8: Handling Merge Conflicts

### Objective
Learn to resolve merge conflicts.

### Tasks

1. Create a new branch:
```bash
git checkout -b update-readme
```

2. Modify README.md:
```bash
echo "## Portfolio Tools" >> README.md
echo "This repository contains portfolio analysis tools." >> README.md
```

3. Commit:
```bash
git add README.md
git commit -m "Add portfolio tools section to README"
```

4. Switch back to main:
```bash
git checkout main
```

5. Modify README.md differently:
```bash
echo "## Risk Analysis Tools" >> README.md
echo "This repository contains risk analysis tools." >> README.md
```

6. Commit:
```bash
git add README.md
git commit -m "Add risk analysis section to README"
```

7. Try to merge:
```bash
git merge update-readme
```

8. You should see a conflict message! View the conflicted file:
```bash
cat README.md
```

9. You'll see conflict markers like:
```
<<<<<<< HEAD
## Risk Analysis Tools
This repository contains risk analysis tools.
=======
## Portfolio Tools
This repository contains portfolio analysis tools.
>>>>>>> update-readme
```

10. Edit README.md to resolve the conflict (keep both sections):
```bash
# Open in your editor and make it look like:
## Portfolio Tools
This repository contains portfolio analysis tools.

## Risk Analysis Tools
This repository contains risk analysis tools.
```

11. Mark as resolved and commit:
```bash
git add README.md
git commit -m "Merge update-readme: combine tool descriptions"
```

12. Push to GitHub:
```bash
git push origin main
```

13. Clean up:
```bash
git branch -d update-readme
```

### Questions to Answer
- What causes merge conflicts?
- How do you know when a conflict is resolved?
- Can conflicts be avoided?

---

## Exercise 9: Viewing History and Differences

### Objective
Practice examining repository history and changes.

### Tasks

1. View full commit history:
```bash
git log
```

2. View compact history:
```bash
git log --oneline
```

3. View history with graph:
```bash
git log --oneline --graph --all
```

4. View commits by a specific author:
```bash
git log --author="Your Name"
```

5. View commits in the last week:
```bash
git log --since="1 week ago"
```

6. View what changed in a specific commit (use a commit hash from your log):
```bash
git show <commit-hash>
```

7. Compare current version with 2 commits ago:
```bash
git diff HEAD~2 HEAD
```

8. View who changed each line of a file:
```bash
git blame portfolio.py
```

### Questions to Answer
- Why is commit history important?
- How can `git blame` help in a team project?
- What information does `git show` provide?

---

## Exercise 10: Undoing Changes

### Objective
Practice various ways to undo changes.

### Tasks

1. Create and modify a file:
```bash
echo "def buggy_function():" > test.py
echo "    return 1 / 0  # Bug!" >> test.py
```

2. See the changes:
```bash
git status
git diff
```

3. **Scenario A: Discard changes before staging**
```bash
# Undo changes to test.py
git checkout -- test.py

# Or with modern syntax:
git restore test.py

# Verify it's gone
git status
```

4. **Scenario B: Unstage a file**
```bash
# Create and stage a file
echo "temporary" > temp.py
git add temp.py

# Unstage it
git reset temp.py

# Check status
git status
```

5. **Scenario C: Undo last commit (keep changes)**
```bash
# Make a commit you want to undo
echo "wrong" > oops.py
git add oops.py
git commit -m "This commit was a mistake"

# Undo the commit but keep the changes
git reset --soft HEAD~1

# Check status - changes are still there but uncommitted
git status

# Clean up
rm oops.py
```

6. **Scenario D: Amend last commit**
```bash
# Commit with a typo in the message
echo "correct" > good.py
git add good.py
git commit -m "Add gud file"

# Fix the commit message
git commit --amend -m "Add good file"

# View the corrected commit
git log --oneline -1
```

### Questions to Answer
- What's the difference between `git reset --soft` and `git reset --hard`?
- When should you use `git commit --amend`?
- Why is `git reset --hard` dangerous?

---

## Exercise 11: Stashing Changes

### Objective
Learn to temporarily save changes.

### Tasks

1. Make some changes:
```bash
echo "# Work in progress" >> portfolio.py
```

2. Check status:
```bash
git status
```

3. Realize you need to switch branches but don't want to commit:
```bash
# Save changes temporarily
git stash

# Check status - working directory is clean
git status
```

4. Do other work:
```bash
git checkout -b hotfix
echo "# Quick fix" >> risk_calculator.py
git add risk_calculator.py
git commit -m "Apply hotfix"
git checkout main
git merge hotfix
git branch -d hotfix
```

5. Bring back your stashed changes:
```bash
# List stashes
git stash list

# Apply the stash
git stash pop

# Check status
git status
```

6. Complete your work:
```bash
git add portfolio.py
git commit -m "Complete work in progress"
git push origin main
```

### Questions to Answer
- When is stashing useful?
- What's the difference between `git stash pop` and `git stash apply`?
- Can you have multiple stashes?

---

## Exercise 12: Creating a .gitignore

### Objective
Learn to exclude files from version control.

### Tasks

1. Create some files that shouldn't be tracked:
```bash
echo "SECRET_KEY=abc123" > .env
mkdir data
echo "user,balance" > data/users.csv
echo "price,volume" > data/prices.csv
touch debug.log
```

2. Check status - see all the untracked files:
```bash
git status
```

3. Create a comprehensive .gitignore:
```bash
cat > .gitignore << EOF
# Secrets
.env
*.key
secrets.txt

# Data files
data/
*.csv

# Logs
*.log

# Python
__pycache__/
*.pyc
*.pyo

# Jupyter
.ipynb_checkpoints/

# OS files
.DS_Store
Thumbs.db

# IDEs
.vscode/
.idea/
*.swp
EOF
```

4. Check status again:
```bash
git status
```
   (The files in .gitignore should not appear)

5. Commit the .gitignore:
```bash
git add .gitignore
git commit -m "Add comprehensive gitignore"
git push origin main
```

### Questions to Answer
- Why is it important not to commit .env files?
- Should you commit .gitignore itself?
- What happens if you committed a file before adding it to .gitignore?

---

## Exercise 13: Collaborative Workflow Simulation

### Objective
Simulate working with a team member.

### Tasks

1. **Simulate a teammate's work on GitHub:**
   - Go to your repository on GitHub
   - Edit hello.py directly on GitHub
   - Change it to:
   ```python
   def greet(name):
       return f"Hello, {name}!"
   
   print(greet("Git"))
   ```
   - Commit with message: "Refactor hello.py into function"

2. **Meanwhile, you've been working locally:**
```bash
# Make different changes to hello.py
echo "# Author: Your Name" > hello.py
echo "print('Hello, Git!')" >> hello.py
echo "print('Learning version control')" >> hello.py

git add hello.py
git commit -m "Add author and extra message"
```

3. **Try to push:**
```bash
git push origin main
```
   (Should get rejected - remote has changes you don't have)

4. **Pull to get remote changes:**
```bash
git pull origin main
```
   (You'll likely have a merge conflict!)

5. **Resolve the conflict:**
   - Open hello.py
   - Resolve the conflict by combining both versions
   - Should end up with something like:
   ```python
   # Author: Your Name
   def greet(name):
       return f"Hello, {name}!"
   
   print(greet("Git"))
   print('Learning version control')
   ```

6. **Complete the merge:**
```bash
git add hello.py
git commit -m "Merge remote changes with local improvements"
git push origin main
```

### Questions to Answer
- Why is it important to pull before pushing?
- How often should you pull from the remote?
- What workflow prevents most conflicts?

---

## Exercise 14: Creating a Pull Request

### Objective
Practice the pull request workflow (like in real team projects).

### Tasks

1. Create a feature branch:
```bash
git checkout -b feature/add-tests
```

2. Create a test file:
```bash
cat > test_portfolio.py << EOF
import portfolio

def test_calculate_return():
    result = portfolio.calculate_return(100, 110)
    assert result == 10.0, "Should return 10% gain"
    
def test_calculate_return_loss():
    result = portfolio.calculate_return(100, 90)
    assert result == -10.0, "Should return 10% loss"

if __name__ == "__main__":
    test_calculate_return()
    test_calculate_return_loss()
    print("All tests passed!")
EOF
```

3. Commit and push the branch:
```bash
git add test_portfolio.py
git commit -m "Add unit tests for portfolio module"
git push -u origin feature/add-tests
```

4. **On GitHub:**
   - You'll see a banner: "Compare & pull request"
   - Click it
   - Title: "Add unit tests for portfolio calculator"
   - Description: "Adds test cases to verify portfolio return calculations"
   - Click "Create pull request"

5. **Review your own PR:**
   - Click "Files changed" tab
   - Review the diff
   - Add a comment on a line
   - Click "Review changes" → "Approve"

6. **Merge the PR:**
   - Click "Merge pull request"
   - Click "Confirm merge"
   - Click "Delete branch" (on GitHub)

7. **Update local repository:**
```bash
git checkout main
git pull origin main
git branch -d feature/add-tests
```

### Questions to Answer
- Why use pull requests instead of pushing directly to main?
- What should you check during a code review?
- When should you require reviews before merging?

---

## Exercise 15: Forking and Contributing

### Objective
Practice contributing to someone else's repository.

### Tasks

1. **Find a repository to contribute to:**
   - Go to: https://github.com/firstcontributions/first-contributions
   - (This is a practice repo for learning to contribute)

2. **Fork the repository:**
   - Click "Fork" button (top right)
   - This creates your own copy

3. **Clone YOUR fork:**
```bash
cd ..  # Go up one level from your practice repo
git clone https://github.com/YOUR-USERNAME/first-contributions.git
cd first-contributions
```

4. **Create a branch:**
```bash
git checkout -b add-your-name
```

5. **Make your contribution:**
   - Follow the instructions in their README
   - Usually involves adding your name to a Contributors.md file

6. **Commit your changes:**
```bash
git add .
git commit -m "Add [Your Name] to Contributors list"
```

7. **Push to YOUR fork:**
```bash
git push -u origin add-your-name
```

8. **Create a Pull Request:**
   - Go to YOUR fork on GitHub
   - Click "Compare & pull request"
   - The base repository should be `firstcontributions/first-contributions`
   - Your fork should be the head repository
   - Create the pull request

9. **Wait for it to be merged!**
   - The maintainers will review and merge your PR
   - Congratulations on your first open source contribution!

### Questions to Answer
- What's the difference between forking and cloning?
- Why fork instead of directly pushing to someone else's repository?
- What happens after your PR is merged?

---

## Final Challenge: Complete Project Workflow

### Objective
Put all your skills together in a realistic project scenario.

### Scenario
You're working on a financial analysis toolkit for FINMA. Create a complete project with proper Git workflow.

### Tasks

1. **Initialize project:**
```bash
cd ..
mkdir finma-toolkit
cd finma-toolkit
git init
```

2. **Set up project structure:**
```bash
# Create directories
mkdir src tests docs data

# Create README
cat > README.md << EOF
# FINMA Financial Analysis Toolkit

## Overview
A Python toolkit for financial analysis and portfolio management.

## Features
- Portfolio return calculations
- Risk analysis
- Performance metrics

## Installation
\`\`\`bash
pip install -r requirements.txt
\`\`\`

## Usage
\`\`\`python
from src.portfolio import calculate_return
result = calculate_return(1000, 1100)
\`\`\`

## License
MIT
EOF

# Create .gitignore
cat > .gitignore << EOF
__pycache__/
*.pyc
.ipynb_checkpoints/
data/*.csv
.env
EOF

# Create requirements.txt
echo "pandas==2.0.0" > requirements.txt
echo "numpy==1.24.0" >> requirements.txt
```

3. **Initial commit:**
```bash
git add .
git commit -m "Initial project setup with structure and README"
```

4. **Create GitHub repository and push:**
   - Create repo on GitHub: `finma-toolkit`
   - Connect and push:
```bash
git remote add origin https://github.com/YOUR-USERNAME/finma-toolkit.git
git push -u origin main
```

5. **Develop Portfolio Module (branch workflow):**
```bash
git checkout -b feature/portfolio-module

# Create portfolio module
cat > src/portfolio.py << EOF
"""Portfolio analysis module"""

def calculate_return(initial_value, final_value):
    """Calculate simple return"""
    return ((final_value - initial_value) / initial_value) * 100

def calculate_cagr(initial_value, final_value, years):
    """Calculate compound annual growth rate"""
    return ((final_value / initial_value) ** (1/years) - 1) * 100
EOF

git add src/portfolio.py
git commit -m "Add portfolio return calculations"
git push -u origin feature/portfolio-module
```

6. **Add tests:**
```bash
cat > tests/test_portfolio.py << EOF
"""Tests for portfolio module"""
import sys
sys.path.insert(0, '../src')
from portfolio import calculate_return, calculate_cagr

def test_calculate_return():
    assert calculate_return(1000, 1100) == 10.0
    assert calculate_return(1000, 900) == -10.0
    print("✓ calculate_return tests passed")

def test_calculate_cagr():
    result = calculate_cagr(1000, 1100, 1)
    assert abs(result - 10.0) < 0.01
    print("✓ calculate_cagr tests passed")

if __name__ == "__main__":
    test_calculate_return()
    test_calculate_cagr()
    print("\n✓ All tests passed!")
EOF

git add tests/test_portfolio.py
git commit -m "Add portfolio module tests"
git push origin feature/portfolio-module
```

7. **Create Pull Request and Merge on GitHub**

8. **Update local main:**
```bash
git checkout main
git pull origin main
git branch -d feature/portfolio-module
```

9. **Develop Risk Module (separate branch):**
```bash
git checkout -b feature/risk-module

cat > src/risk.py << EOF
"""Risk analysis module"""
import statistics

def calculate_volatility(returns):
    """Calculate standard deviation of returns"""
    return statistics.stdev(returns)

def calculate_sharpe_ratio(returns, risk_free_rate=0.02):
    """Calculate Sharpe ratio"""
    avg_return = statistics.mean(returns)
    volatility = calculate_volatility(returns)
    return (avg_return - risk_free_rate) / volatility
EOF

git add src/risk.py
git commit -m "Add risk analysis functions"

# Add tests
cat > tests/test_risk.py << EOF
"""Tests for risk module"""
import sys
sys.path.insert(0, '../src')
from risk import calculate_volatility, calculate_sharpe_ratio

def test_calculate_volatility():
    returns = [0.01, 0.02, -0.01, 0.03, 0.02]
    vol = calculate_volatility(returns)
    assert vol > 0
    print("✓ calculate_volatility test passed")

def test_calculate_sharpe_ratio():
    returns = [0.05, 0.07, 0.03, 0.06, 0.08]
    sharpe = calculate_sharpe_ratio(returns)
    assert sharpe > 0
    print("✓ calculate_sharpe_ratio test passed")

if __name__ == "__main__":
    test_calculate_volatility()
    test_calculate_sharpe_ratio()
    print("\n✓ All risk tests passed!")
EOF

git add tests/test_risk.py
git commit -m "Add risk module tests"
git push -u origin feature/risk-module
```

10. **Merge via Pull Request on GitHub**

11. **Create Documentation:**
```bash
git checkout main
git pull origin main
git checkout -b docs/add-examples

cat > docs/examples.md << EOF
# Examples

## Portfolio Analysis

\`\`\`python
from src.portfolio import calculate_return, calculate_cagr

# Calculate simple return
return_pct = calculate_return(10000, 11500)
print(f"Return: {return_pct}%")  # Output: Return: 15.0%

# Calculate CAGR
cagr = calculate_cagr(10000, 15000, 3)
print(f"CAGR: {cagr:.2f}%")
\`\`\`

## Risk Analysis

\`\`\`python
from src.risk import calculate_volatility, calculate_sharpe_ratio

# Calculate volatility
returns = [0.05, 0.07, 0.03, 0.06, 0.08]
vol = calculate_volatility(returns)
print(f"Volatility: {vol:.4f}")

# Calculate Sharpe ratio
sharpe = calculate_sharpe_ratio(returns, risk_free_rate=0.02)
print(f"Sharpe Ratio: {sharpe:.2f}")
\`\`\`
EOF

git add docs/examples.md
git commit -m "Add usage examples documentation"
git push -u origin docs/add-examples
```

12. **Final merge and tag release:**
```bash
# Merge via GitHub PR
git checkout main
git pull origin main

# Tag version 1.0.0
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin v1.0.0
```

13. **View your project history:**
```bash
git log --oneline --graph --all
```

### Congratulations! 🎉
You've completed a full project workflow using Git and GitHub!

---

## Completion Checklist

Mark each exercise as complete:

- [ ] Exercise 1: Initial Setup
- [ ] Exercise 2: First Repository
- [ ] Exercise 3: Multiple Commits
- [ ] Exercise 4: Connect to GitHub
- [ ] Exercise 5: Pull-Modify-Push
- [ ] Exercise 6: Working with Branches
- [ ] Exercise 7: Merging Branches
- [ ] Exercise 8: Handling Conflicts
- [ ] Exercise 9: Viewing History
- [ ] Exercise 10: Undoing Changes
- [ ] Exercise 11: Stashing Changes
- [ ] Exercise 12: Creating .gitignore
- [ ] Exercise 13: Collaborative Workflow
- [ ] Exercise 14: Pull Requests
- [ ] Exercise 15: Forking
- [ ] Final Challenge: Complete Project

---

## Additional Practice

### Daily Practice Routine
1. Pull before starting work
2. Create feature branches for changes
3. Commit with clear messages
4. Push regularly
5. Review your git log

### Common Mistakes to Avoid
1. ❌ Working directly on main branch
2. ❌ Making huge commits with unrelated changes
3. ❌ Writing vague commit messages
4. ❌ Forgetting to pull before push
5. ❌ Committing sensitive data

### Good Habits to Develop
1. ✅ Commit often with logical units of work
2. ✅ Write descriptive commit messages
3. ✅ Pull before starting work
4. ✅ Use branches for features
5. ✅ Review changes before committing

---

## Next Steps

1. **Practice daily:** Use Git for ALL your coursework
2. **Contribute to open source:** Find beginner-friendly projects
3. **Collaborate:** Work on a group project using Git
4. **Learn advanced features:** Rebase, cherry-pick, bisect
5. **Explore GitHub features:** Actions, Projects, Issues

**Remember:** The best way to learn Git is to use it every day!

Good luck with your Git journey! 🚀
