#### Date: 7th November 2025
# Git Refresher

## 1. What is Git?
Git is a distributed version control system (DVCS) that tracks changes in any 
set of computer files, usually being used for coordinating work among 
programmers collaboratively developing source code during software development.

## 2. Fundamental Concepts
- **Repository (Repo):** A folder that contains all project files and their 
  revision history.
- **Commit:** A snapshot of your project at a specific point in time.
- **Branch:** A separate line of development.
- **Merge:** Combining changes from different branches.
- **Pull Request (PR):** Proposing changes to a repository.

## 3. Basic Commands
- `git init`: Initialize a new Git repository.
- `git clone <url>`: Copy a remote repository to your local machine.
- `git status`: Show the status of your working directory.
- `git add <file>`: Stage changes for the next commit.
- `git commit -m "message"`: Record changes in the repository.

## 4. Working with Remotes
- `git remote add origin <url>`: Connect local repo to a remote repo.
- `git push origin <branch>`: Upload local branch commits to the remote.
- `git pull origin <branch>`: Fetch and merge changes from the remote.
- `git fetch`: Download changes from the remote without merging.

## 5. Branching and Merging
- `git branch`: List local branches.
- `git checkout -b <name>`: Create and switch to a new branch.
- `git switch <name>`: Switch to an existing branch.
- `git merge <branch>`: Merge another branch into the current one.
- `git branch -d <name>`: Delete a local branch.

## 6. Undoing Changes
- `git checkout -- <file>`: Discard changes in a file.
- `git reset HEAD <file>`: Unstage a staged file.
- `git reset --soft HEAD~1`: Undo the last commit but keep changes staged.
- `git reset --hard HEAD~1`: Undo the last commit and discard all changes.
- `git revert <commit_id>`: Create a new commit that undoes a previous one.

## 7. Stashing
Temporarily save uncommitted changes to work on something else:
- `git stash`: Save changes.
- `git stash pop`: Apply saved changes and remove from stash.
- `git stash list`: View all stashes.

## 8. Log and Diff
- `git log`: View commit history.
- `git log --oneline`: Condensed history view.
- `git diff`: View changes between working directory and the index.
- `git diff --staged`: View changes between index and the last commit.

## 9. Best Practices
- **Commit Often:** Small, logical changes are easier to manage.
- **Write Good Commit Messages:** Use the imperative mood (e.g., "Add feature" 
  not "Added feature").
- **Don't Commit Secrets:** Use `.gitignore` to exclude sensitive files like 
  API keys or credentials.
- **Pull Before Push:** Always ensure you have the latest changes from the 
  remote.

## 10. Conclusion
Git is an indispensable tool in the DevOps toolchain. It allows for seamless 
collaboration, easy experimentation via branching, and provides a safety net for 
code history.

---
*End of Notes*
