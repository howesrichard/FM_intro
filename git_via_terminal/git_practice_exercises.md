# Git and GitHub Practice Exercises

## Overview

These hands-on exercises will help you practice essential Git and GitHub commands. Complete them in order, as later exercises build on earlier ones.

**Time required:** 2-3 hours  
**Prerequisites:** Git installed, GitHub account created


---

## Exercise 1: Creating Your First Repository

### Objective
Create a Git repository using the browser and make your first commit.

### Tasks

1. Create a new repo for your project:
Github > New > Name: "{Your name}_finma_git_practice", Private visibility, Yes README.md

2. Create a new codespace, this will take a few minutes to configure.

3. Check the status:
```bash
git status
```

4. Add details into the README.md file e.g.
```markdown

## This is a practice repo made by {your name} to practice using git. 

About me, my favourite place to travel is {location}
```

5. Check status again:
```bash
git status
```
As you can see, README.md file has changed (as you added some lines in), and is colour red. 
In this instance, it is not officially part of the repo unless we are ready to add it in via staging and commiting.

6. Add the README to staging:
```bash
git add README.md
```

7. Check status once more:
```bash
git status
```

As you can see, README.md file has changed status from red to green since it staged/ready to be added. Why? It gives git a list of files of which files you are ready to commit to add into the repo.

8. Commit the file:
```bash
git commit -m "Initial commit: Add README"
```
Add a message describing what you have changed. Make sure the message is clear and not keyboard spam for the sake of a message, as the purpose is for collaboration and for teammates to understand what you have changed :).

9. Commit the file:
```bash
git push
```
Now the updated README.md file is officially added to your repo in the main branch.

10. View the commit history:
```bash
git log
```

### Questions to Answer
- What does "untracked file" mean?
- What information is shown in the git log output?

---

## Exercise 2: Working with Branches (o do)

### Objective
Learn to create and work with branches.

### Tasks

1. Create a new branch on github browser
   <img width="677" height="388" alt="New branch" src="https://github.com/user-attachments/assets/d3935034-b823-4d47-8a79-23003f72620e" />

2. Verify you're on the new branch:
```bash
git branch
```

3. Create a new file on this branch:

5. Add and commit:
```bash
git add test.py
git commit -m "Add test.py"
```

6. Push the new branch to GitHub:
```bash
git push
```

8. Verify the file isn't there in main via browser


### Questions to Answer
- Why use branches instead of working directly on main?
- What happens to your files when you switch branches?
- How can you see all branches, including remote ones?

---

## Exercise 3: Merging Branches and creating a pull request

### Objective
Practice merging a branch back into main.

### Tasks

1. Make sure you're on the branch:

2. Add another line to test.py:

3. Add and commit:
```bash
git add test.py
git commit -m "Add text about {description}"
```

4. Push to GitHub:
```bash
git push
```

5. Create a new pull request from your branch to main.

**On GitHub:**
   - You'll see a banner: "Compare & pull request"
   - Click it
   - Title: 
   - Description: 
   - Click "Create pull request"

**Review your own PR:**
   - Click "Files changed" tab
   - Review the diff
   - Add a comment on a line
   - Click "Review changes" → "Approve"

**Merge the PR:**
   - Click "Merge pull request"
   - Click "Confirm merge"
   - Click "Delete branch" (on GitHub)

7. (optional) Delete the non-main branch (it's now merged):

### Questions to Answer
- What does "fast-forward merge" mean?
- When might you see a merge conflict?
- Why delete branches after merging?

---

## Exercise 4: Handling Merge Conflicts

### Objective
Learn to resolve merge conflicts.

### Tasks

1. Create a new branch
   
2. Modify README.md entirely:
```markdown
## Portfolio Tools
This repository contains portfolio analysis tools
```

3. Commit:
```bash
git add README.md
git commit -m "Add portfolio tools section to README"
```

4. Switch back to main's codespace

5. Modify README.md differently:
```markdown
## Risk Analysis Tools"
This repository contains risk analysis tools
```

6. Commit:
```bash
git add README.md
git commit -m "Add risk analysis section to README"
```

7. Try to merge:
```bash
git merge {branch}
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

## Exercise 5: Forking and Contributing (to 

### Objective
Practice contributing to someone else's repository.

### Tasks

1. **Find a repository to contribute to:**
   - Go to: https://github.com/firstcontributions/first-contributions
   - (This is a practice repo for learning to contribute)

2. **Fork the repository:**
   - Click "Fork" button (top right)
   - This creates your own copy

3. **Create a branch or main:**

4. **Make your contribution:**
   - Follow the instructions in their README
   - Usually involves adding your name to a Contributors.md file

5. **Commit your changes:**
```bash
git add .
git commit -m "Add [Your Name] to Contributors list"
git push
```

6. **Create a Pull Request:**
   - Go to YOUR fork on GitHub
   - Click "Compare & pull request"
   - The base repository should be `firstcontributions/first-contributions`
   - Your fork should be the head repository (either branch or main depending on what you used. If you used a branch try to merge it into your fork's main first)
   - Create the pull request

7. **Wait for it to be merged!**
   - The maintainers will review and merge your PR
   - Congratulations on your first open source contribution!

### Questions to Answer
- What's the difference between forking and cloning?
- Why fork instead of directly pushing to someone else's repository?
- What happens after your PR is merged?

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
