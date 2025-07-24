GITHUB ACTIONS CI CD NOTES

# Initialize local repository
git init

# Add a specific file to staging
git add .\githubActionsNotes.md

# Set your Git identity globally
git config --global user.email "niwalkar.jogesh@gmail.com"
git config --global user.name "jogeshniwalkar"

# Check current branch
git branch

# Attempt to push (fails because no remote set yet)
git push

# Add remote origin (GitHub repo)
git remote add origin https://github.com/jogeshniwalkar/ci-cd-github-action.git

# Check remote (optional, not executed but helpful)
git remote -v

# Add all files to staging
git add .

# Check git status (see what’s staged, etc.)
git status

# First commit
git commit -m "initial commit"

# Push & set upstream to origin/master (first-time push)
git push --set-upstream origin master

# Check local branch again (confirmation)
git branch


# Check commit history
git log

# Create new branch
git checkout -b feature/my-feature

# Switch to an existing branch
git checkout master

# View detailed branch info
git branch -vv

# View remote URL
git remote get-url origin

# Change default branch to main (optional)
git branch -M main



✅ Scenario Recap:
1. You took a fresh pull from develop.
2. Created a feature/my-feature branch.
3. Worked for 3 days and made local commits.
4. Meanwhile, develop has progressed with new commits from 
other teammates (including conflicting changes on shared files).
5. You're now getting merge conflicts when trying to create
a PR or push your branch.

**🧠 Goal:**
Safely bring the latest develop into your feature branch, resolve merge conflicts locally, and then push your updated feature branch for PR creation.



# Step-by-Step Git Commands:
1. Stash or Commit Uncommitted Changes (if any)
git status  # Check for uncommitted files
# If uncommitted work exists, either commit it:
git add .
git commit -m "WIP: Saving progress before merge"

# OR stash it if you don't want to commit yet:
git stash
2. Fetch Latest Changes from Remote

git fetch origin
3. Merge Latest develop into Your Feature Branch
This brings all latest changes from develop to your branch.
git checkout feature/my-feature
git merge origin/develop
You will now see merge conflicts in common files.

4. Resolve Merge Conflicts
Edit the conflicted files manually. Look for <<<<<<<, =======, and >>>>>>> markers and update them appropriately.
Once resolved:
bash
git add <conflicted-files>
After all conflicts are resolved and added:

git commit  # This creates a merge commit
5. (Optional) Test After Merge
Run your local build, unit tests, or app to confirm everything still works.

6. Push Your Feature Branch
git push origin feature/my-feature
Now you can open your Pull Request from feature/my-feature → develop.

 Step-by-Step Git Commands:
1. Stash or Commit Uncommitted Changes (if any)
bash
Copy
Edit
git status  # Check for uncommitted files

# If uncommitted work exists, either commit it:
git add .
git commit -m "WIP: Saving progress before merge"

# OR stash it if you don't want to commit yet:
git stash
2. Fetch Latest Changes from Remote
bash
Copy
Edit
git fetch origin
3. Merge Latest develop into Your Feature Branch
This brings all latest changes from develop to your branch.

bash
Copy
Edit
git checkout feature/my-feature
git merge origin/develop
You will now see merge conflicts in common files.

4. Resolve Merge Conflicts
Edit the conflicted files manually. Look for <<<<<<<, =======, and >>>>>>> markers and update them appropriately.

Once resolved:

bash
Copy
Edit
git add <conflicted-files>
After all conflicts are resolved and added:

bash
Copy
Edit
git commit  # This creates a merge commit
5. (Optional) Test After Merge
Run your local build, unit tests, or app to confirm everything still works.

6. Push Your Feature Branch
bash
Copy
Edit
git push origin feature/my-feature
Now you can open your Pull Request from feature/my-feature → develop.

**🧼 Optional: Use rebase Instead of merge (Cleaner History)**
If your team prefers linear commit history, you can rebase instead of merging:

bash
Copy
Edit
git checkout feature/my-feature
git fetch origin
git rebase origin/develop
You will still get merge conflicts, but you’ll resolve them one commit at a time during rebase.

After rebase completes:

bash
Copy
Edit
git push origin feature/my-feature --force-with-lease
⚠️ Use --force-with-lease only if you understand that this rewrites history (safe if only you are working on this branch).


If your team prefers linear commit history, you can rebase instead of merging:

git checkout feature/my-feature
git fetch origin
git rebase origin/develop
You will still get merge conflicts, but you’ll resolve them one commit at a time during rebase.

After rebase completes:
git push origin feature/my-feature --force-with-lease
⚠️ Use --force-with-lease only if you understand that this rewrites history (safe if only you are working on this branch).



