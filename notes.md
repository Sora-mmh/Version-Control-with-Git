# Git Commands

## 1. Repository Management

- **Initialize a new repo**
  ```sh
  git init
  ```

- **Clone a repository**
  ```sh
  git clone 
  ```

- **View the git configuration**
  ```sh
  git config --list
  git config user.name "Your Name"
  git config user.email "you@example.com"
  ```

## 2. Basic Workflow (Staging & Committing)

- **Check status**
  ```sh
  git status
  ```

- **Add files to staging area**
  ```sh
  git add 
  git add .                # Add all changes in the current directory
  ```

- **Commit staged changes**
  ```sh
  git commit -m "commit message"
  ```

- **Commit and amend the last commit (edit message or staged files)**
  ```sh
  git commit --amend
  ```

- **View commit history**
  ```sh
  git log
  git log --oneline --graph --decorate
  git log -p         # See history for a file
  ```

## 3. Branching

- **List branches**
  ```sh
  git branch                # Local
  git branch -r             # Remote
  git branch -a             # All (local & remote)
  ```

- **Create branch**
  ```sh
  git branch 
  ```

- **Checkout branch (older versions)**
  ```sh
  git checkout 
  git checkout -b   # Create and switch
  ```

- **Delete local branch**
  ```sh
  git branch -d 
  git branch -D      # Force delete
  ```

- **Delete remote branch**
  ```sh
  git push -d origin 
  git push origin --delete 
  ```

- **Rename current branch**
  ```sh
  git branch -m 
  ```

## 4. Remote Repositories

- **List remotes**
  ```sh
  git remote -v
  ```

- **Add a new remote**
  ```sh
  git remote add origin 
  ```

- **Remove a remote**
  ```sh
  git remote rm 
  ```

## 5. Fetching & Synchronization

- **Fetch latest changes**
  ```sh
  git fetch
  ```

- **Fetch and prune deleted branches**
  ```sh
  git fetch --prune
  ```

- **Download and integrate changes**
  ```sh
  git pull                        # fetch + merge
  git pull --rebase               # fetch + rebase local commits
  ```

- **Push changes**
  ```sh
  git push origin           # Push branch to remote
  git push -u origin        # Set upstream for branch
  git push                          # Push current branch and tracking info
  ```

## 6. Merging and Rebasing

- **Merge another branch into current**
  ```sh
  git merge 
  git merge --no-ff       # Force a merge commit (no fast-forward)
  git merge --abort               # Abort conflicted merge
  ```

- **Rebase onto another branch**
  ```sh
  git rebase 
  git rebase -i    # Interactive (edit, squash, reorder commits)
  git rebase --continue           # Complete after conflict
  git rebase --abort              # Abort a rebase in progress
  ```

## 7. Resetting, Reverting & Undoing Changes

- **Unstage a file**
  ```sh
  git reset                 # Unstage
  ```

- **Reset to previous commit**
  ```sh
  git reset --soft HEAD~1         # Keep changes staged
  git reset --mixed HEAD~1        # Keep changes, unstaged (default)
  git reset --hard HEAD~1         # Discard all changes
  ```

- **Restore file to a previous version**
  ```sh
  git checkout  -- 
  git restore                   # Unstage and revert changes (Git 2.23+)
  git restore --staged 
  ```

- **Revert a commit (safe for public branches)**
  ```sh
  git revert 
  git revert HEAD~2..HEAD             # Revert a range
  ```

- **Remove untracked files**
  ```sh
  git clean -f                # Remove untracked files
  git clean -fd               # Remove untracked files and directories
  ```

## 8. Cherry-Picking

- **Apply a commit from another branch onto current**
  ```sh
  git cherry-pick 
  git cherry-pick  
  ```

## 9. Stashing

- **Stash changes for later**
  ```sh
  git stash              # Stash local, not yet staged changes
  git stash -u           # Include untracked files
  git stash pop          # Apply the latest stash and remove from stack
  git stash list         # List all stashes
  git stash apply    # Apply specific stash
  ```

## 10. Tagging

- **List tags**
  ```sh
  git tag
  ```

- **Create a tag**
  ```sh
  git tag 
  git tag -a  -m "message"
  ```

- **Push tags**
  ```sh
  git push origin 
  git push origin --tags        # Push all tags
  ```

- **Delete tag**
  ```sh
  git tag -d 
  git push origin --delete 
  ```

## 11. Gitignore & Attributes

- **List which .gitignore rule is responsible**
  ```sh
  git check-ignore -v 
  ```

- **Remove tracked files that should now be ignored**
  ```sh
  git rm -r --cached 
  git commit -m "Remove tracked ignored files"
  git push
  ```

## 12. Conflict and Collaboration Tools

- **View unresolved conflicts**
  ```sh
  git status
  ```

- **After conflict resolution**
  ```sh
  git add 
  git commit                     # Complete merge
  git rebase --continue          # After editing
  git merge --abort              # Cancel the merge
  git diff                       # See conflicting changes
  git mergetool                  # Use merge tool
  ```

- **Useful log/diff commands**
  ```sh
  git show 
  git diff  
  git blame                 # See line authorship
  ```

## 13. Miscellaneous

- **View remote URL**
  ```sh
  git remote get-url origin
  ```

- **Show reference log (recover "lost" branches/commits)**
  ```sh
  git reflog
  ```

- **Squash commits interactively**
  ```sh
  git rebase -i HEAD~3
  ```

# Best Practices and Practical Tips

- **Commit often, with clear messages.**
- **Always pull (fetch+merge/rebase) before pushing or when starting new work.**
- **Keep branches short-lived and up to date with main.**
- **Use `git status` after every major step.**
- **Resolve conflicts carefully—remove conflict markers and stage files after fix.**
- **Never rewrite shared/public history except with explicit team agreement.**
- **Interactive rebase (`git rebase -i`) is great for cleaning commit history before merging.**
- **Use `git stash` to quickly move local work aside when changing branches or pulling.**
- **Use `git log --oneline --graph --decorate --all` to view the project tree visually.**
