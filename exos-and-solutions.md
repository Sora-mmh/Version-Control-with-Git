# Version Control with Git — Exercises & Solutions

This document contains practical Git exercises and their step-by-step solutions.  
You’ll learn cloning repositories, branching, merging, fixing conflicts, reverting, resetting, and cleaning up branches.

**Repository to use:**  
[GitLab — git-exercises](https://gitlab.com/twn-devops-bootcamp/latest/03-git/git-exercises)  

***

## Exercise 1: Clone and Create New Repository

**Task:**  
- Clone the provided Git repository locally.  
- Re-initialize it as your own repository and push it to a **new GitLab repo**.

**Solution:**
```sh
# clone repository & change into project directory
git clone git@gitlab.com:twn-devops-bootcamp/latest/03-git/git-exercises.git
cd git-exercises

# remove reference to the old remote and initialize as a new local repo
rm -rf .git
git init
git add .
git commit -m "Initial commit"

# add your remote GitLab repository and push
git remote add origin git@gitlab.com:{gitlab-user}/{gitlab-repo}.git
git push -u origin master
```

***

## Exercise 2: `.gitignore`

**Task:**  
- Ignore IDE/editor-specific files and build folders:
  - `.idea`
  - `.DS_Store`
  - `out`
  - `build`
- Remove them from Git tracking if already committed.

**Solution:**
```sh
# .gitignore file content
.idea
.DS_Store
out
build
```

```sh
# remove already committed files/folders from Git cache
git rm --cached .DS_Store
git rm -r --cached .idea
git rm -r --cached out
git rm -r --cached build

# commit and push changes
git add .
git commit -m "Remove ignored files"
git push
```

***

## Exercise 3: Feature Branch

**Task:**  
- Create a `feature/changes` branch.  
- In `build.gradle`, update `logstash-logback-encoder` to version `7.3`.  
- In `src/main/webapp/index.html`, add the provided image.  
- Commit descriptively and push.

**Solution:**
```sh
# create and switch to feature branch
git checkout -b feature/changes

# edit build.gradle (line 18)
compile group: 'net.logstash.logback', name: 'logstash-logback-encoder', version: '7.3'

# edit index.html (line 9)


# check and commit
git diff
git add .
git commit -m "Upgrade logback library and add image url"
git push
```

***

## Exercise 4: Bugfix Branch

**Task:**  
- Create a `bugfix/changes` branch.  
- Fix a spelling error in `Application.java` (line 22).  
- Commit and push.

**Solution:**
```sh
git checkout -b bugfix/changes

# in Application.java
log.info("Java app started");

git diff
git add .
git commit -m "Fix spelling error"
git push
```

***

## Exercise 5: Merge Request

**Task:**  
- Merge `feature/changes` into `master` (e.g., via GitLab UI).

**Solution (CLI alternative):**
```sh
git checkout master
git merge feature/changes
git push
```

***

## Exercise 6: Fix Merge Conflict

**Task:**  
- On `bugfix/changes`, update `logstash-logback-encoder` to version `7.2`.  
- Merge `master` into `bugfix/changes` and resolve conflicts.

**Solution:**
```sh
git checkout bugfix/changes

# update dependency in build.gradle
compile group: 'net.logstash.logback', name: 'logstash-logback-encoder', version: '7.2'

git add .
git commit -m "Upgrade logger library version"

# merge master into bugfix branch
git merge master

# fix merge conflicts (build.gradle), then:
git status
git add .
git commit

# push merge resolution
git push
```

***

## Exercise 7: Revert Commit

**Task:**  
- On `bugfix/changes`, fix a spelling error in `index.html`.  
- Change the image URL in a separate commit.  
- Revert the last commit because the previous image was correct.

**Solution:**
```sh
# fix spelling error
Sarah - Full stack developer
git add .
git commit -m "Fix spelling error"

# update image URL

git add .
git commit -m "Set image url"

# push both commits
git push

# revert last commit
git revert HEAD
git push
```

***

## Exercise 8: Reset Commit

**Task:**  
- Locally commit a change to Bruno's role, then undo it before pushing.

**Solution:**
```sh
# adjust Bruno's role in index.html
Bruno - DevOps engineer

git add .
git commit -m "Adjust employee role description"

# reset (undo) last commit locally
git reset --hard HEAD~
```

***

## Exercise 9: Merge Without Merge Request

**Task:**  
- Merge `bugfix/changes` directly into `master` via CLI (ensure master is up-to-date first).

**Solution:**
```sh
git checkout master
git merge bugfix/changes
git push
```

***

## Exercise 10: Delete Branches

**Task:**  
- Delete `feature/changes` and `bugfix/changes` both locally and remotely.

**Solution:**
```sh
# delete locally
git branch -D bugfix/changes
git branch -D feature/changes

# delete remotely (CLI alternative — or use GitLab UI)
git push origin --delete bugfix/changes
git push origin --delete feature/changes
```
