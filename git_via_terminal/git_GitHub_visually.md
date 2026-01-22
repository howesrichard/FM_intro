# A visual explanation of git and GitHub

## What is git
Git is a version controls system.   It tracks changes to files over time allowing you to:
- Save snapshots (commits) of your project at any point
- Compare commits to see what's changed
- Revert to previous versions if needed
- See who changed what and when
- Work on multiple features simultaneously (branches)
- Collaborate with others without overwriting each other's work

### Commits are a series of snapshots

![Git Commit History](assets/git_commit_history.png)


## Screenshots of a illustrative workflow

Our initial commit contained only a redme file.   In our second commit we add a line to the readme.
![M2 Change to README](assets/m2_change_to-readme.png)

In our third commit we add another line.   You can see the changes tracked between commits.   git diff is the command to bring this up.   Or you can click on the commit in the graph and the particular file you want to inspect changes on.
![M3 New Comment in README](assets/m3_new_comment_in_readme.png)


Now we use the git push command to publish this latest commit to the GitHub.

![Git Push or Sync](assets/git_push_OR_sync.png)

Now we create a new branch and call it "feature".

![Create Feature Branch](assets/create_feature_branch.png)

On this branch we create an new python file (we commit this as our 5th commit so far but this time to a new branch).   Then we enhance the function and commit this change to the feature branch. 
![M6 Enhance Function](assets/m6_enhance_function.png)

Now we create a Pull Request in order to merge our new feature into the main branch.
![Pull Request](assets/pull_request.png)

And then we merge it with a merge commit.
![Merge PR](assets/merge_PR.png)

Now we switch back the the main branch.   Here you can see the history of our feature branch which is now merged.

![Checkout Main](assets/checkout_main.png)

Lets make another readme change.

![Parallel README Change](assets/paralell%20readme%20change.png)

Now we create a new branch "tester" to create a jupyter notebook to test the new function.
![Tester Changes](assets/tester_changes.png)

And yet another branch, "another-feature", to make another function within our .py file.
![Another Function](assets/another_function.png)

After we do a pull request for each of these and merge them in, you can see the parallel development displayed on the graph.

![Parallel Changes](assets/paralell%20changes.png)







