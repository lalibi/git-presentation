layout: true
name: inverse
class: center, middle, inverse

---
# [Git]

---
## What is it?

- (D)VCS = (Distributed) Version Control System
- SCM = Source Code/Control Management

--

D = Distributed = No SPoF

---
## History

- SCSS
- RCS
- CVS
- SVN
- Visual SourceSafe

---
## Other options

- Mercurial (Hg)

---
layout:true

## Configuration

### System wide

```bash
%PROGRAMFILES%\Git\etc\gitconfig
```

---
### Only for current User (Global)

```bash
%USERPROFILE%\.gitconfig
```

---
### Project wide

```bash
<project-folder>\.git\config
```

---
layout: true

## `git config`

---
```bash
git config --system ...

git config --global ...
```

---

```bash
git config --global user.name "Some Name"

git config --global user.email "some.email@example.com"
```

---
```bash
git config --list

git config --list --global
```

---
```bash
git config --global core.editor "notepad.exe"

git config --global color.ui true
```

---
layout: true

## `git help`

---
```bash
git help

git help <command-name>
```

* Use <kdb>f</kdb>, <kdb>b</kdb>, <kdb>q</kdb> to navigate

---
layout: true

## `git init`

---
layout: true

## `git add`

---
```bash
git add .

git add <folder-name>/

git add <file-name>

git add <file-name-1> <file-name-2>
```

---
layout: true

## `git commit`

---
```bash
git commit -m "Some message"

git commit -a                           # add & commit

git commit -am "Some mesasge"           # add & commit w/ message 

git commit --ammend -m "Some message"   # Repair message
```

--

- Adds all changes
- Doesn't include unstaged and deleted
    - +modified -new -deleted

---
layout: true

## `git log`

---
```bash
git log -10                 # 10 last commits

git log --since=2017-01-01

git log --until=2017-12-31

git log --since="2 weeks ago" --until="3 days ago"

git log --author="John Doe"

git log --grep="Init"       # Case Sensitive

git log --oneline

git log <SHA-1>..<SHA-2>    # Range

git log -p                  # Patch mode, see diffs

git log --stat --summary

git log --graph

git log --oneline --graph --all --decorate
```
---
layout: false

## Two-tree / Three-tree architecture

---
layout: false

## `SHA` values

- 40 char `SHA-1` checksums

---
layout: false

## `HEAD`

- Points to the next commit, in the current branch

---
layout: true

## `git status`

---
```bash
git status
```
---
layout: true

## `git diff`

---
```bash
git diff            # working directory

git diff --staged   # staging index, previously --cached

git diff --color-words
```

---
layout: true

## `git rm`

---
```bash
git rm <file-name>

git rm --cached <file-name>     # Removes from a file from the staging index, but not the working directory

```
---
layout: true

## `git mv`

---
```bash
git mv <old-file-name> <new-file-name>
```
---
layout: true

## `git reset`

---
```bash
git checkout -- <file-name>     # Discard changes

git reset HEAD <file-name>      # Unstage changes
```

---
```
git reset --soft    # Doesn't change working directory or staging index

git reset --mixed   # Doesn't change working directory, changes staging index to match repository

git reset --hard    # Changes working directory and staging index to match repository
```
---
layout: true

## `git revert`

---
```bash
git revert <SHA>
```
---
layout: true

## `git clean`

---
```bash
git clean -n    # Dry run

git clean -f    # Force
```

--

Discard changes **but only** grom working directory (i.e. untracked changes)

---
layout: true

## `.gitignore`

---

### Wildcards

- ?
- [aeiou
- [0-9]

---
### Examples

```
 *.zip 
 !db.zip
 assets/videos/
```

---
### Global excludes

```bash
git config --global core.excludefile <path-to-file> # %USERPROFILE%\.gitignore_global
```

---
layout: true

## `git ls-tree` & tree-ish

---
```bash
git ls-tree HEAD

git ls-tree HEAD^

git ls-tree HEAD~2

git ls-tree master

git ls-tree master assets/

git ls-tree <SHA>
```

---
layout: true

## `git show`

---

```bash
git show <tree-ish>     # Usually <SHA>
```

---
layout: true

## `git diff`

---

```bash
git diff

git diff --staged

git diff <tree-ish>

git diff <tree-ish> <file-name>

git diff <tree-ish-1>..<tree-ish-2>     # Range

git diff --stat --summary

git diff --ignore-space-change          # abbrev: -b

git diff --ignore-all-space             # abbrev: -w

git diff --color-words
```

---
layout: true

## `git branch`

---

```bash
git branch                  # Show list

git branch <branch-name>

git branch

git branch --merged         # Show all branches that are completely included in the current one

git branch -m <old-branch-name> <new-branch-name> # Rename a branch

git branch -d <branch-name> # Delete a branch, won't delete if current branch **or** it has commits

git branch -D <branch-name> # Force delete
```

---
layout: true

## `git checkout`

---

```bash
git checkout <branch-name>

git checkout -b             # Create & Chekout brach

git checkout -- <file-name> # Discard changes for file, -- = current branch
```

---
### Example workflow

```
git branch <new-feature-branch>
git branch
git checkout <new-feature-branch>
# Make some changes
git commit -m "Some message"
git diff master
git checkout master
# Make some changes
git commit -am "Some message"
git diff <new-feature-branch> --color-words

```

---
layout: true

## `git merge`

---

```bash
git merge <branch-name>           # Execute from the receiving branch, that needs to be clean.

git merge --no-ff <branch-name>   # Force a branch commit, ff = fast-forward

git merge --ff-only <branch-name> # Do it only if it can be done as ff

git merge --abort
```

---
### Example workflow

```bash
git merge <branch-name>
<CONFLICT>
<EDIT FILE MANUALLY>
git add <file-name>
git commit  # Git provides a default merge message
```
---
layout: true

## `git stash`

---

```bash
git stash

git stash save "Stash name"

git stash --include-untracked-files # -u

git stash list

git stash show <stash-ref>

git stash show -p <stash-ref> # Patch mode

git stash pop                 # Apply & delete latest one

git stash apply               # Apply but don't delete

git stash drop

git stash clear # Drops all stashes
```

---
layout: true

## `git remote`

---

```bash
git remote  # List all remote repos

git remote add <alias> <url>    # Usually alias = `origin`

git remote -v                   # Verbose

git remote rm <alias>           # Remove a remote repos   
```

---
layout: true

## `git push` & `git branch`

---

```bash
git push -u <alias> <branch-name>   # Usually `origin master`, -u = --set-upstream (sets tracking)

git push                            # If tracking/upstream is already set up

git branch -r   # Show remote branches

git branch -a   # Show all branches
```

---
layout: true

## `git clone`

---

```bash
git clone <url> # Only the default branch, usually `master`

git clone <url> <folder-name>

git clone -b <branch-name> <url>
```

---
layout: true

## Tracking remote branches

```bash
git push -u ...

git config branch.<branch-name>.remote ...

git config branch.<branch-name>.merge ...
```

---
layout: true

## Working w/ remote repos

```bash
git log --oneline origin/master

git diff master..origin/master --color-words

git dif  origin/master..master

git log --oneline -5 origin/master

git branch -r

```

---
layout: true

## `git fetch`

---

```bash
git fetch

git fetch <remote-name> # When it's different from `origin`
```

--

- Fetch is safe, updates only `origin/master`
- Fetch often
- Fetch before push
- Fetch before merge


---
layout: true

## `git pull`

---

### git pull = git fetch & git merge

---
```bash
git pull
```

---
layout: false

## Usefull links

- ![](https://www.google.com/s2/favicons?domain=help.github.com) [Set Up Git - User Documentation](https://help.github.com/articles/set-up-git/)
- ![](https://www.google.com/s2/favicons?domain=help.github.com) [Ignoring files - User Documentation](https://help.github.com/articles/ignoring-files/)
    - ![](https://www.google.com/s2/favicons?domain=github.com) [github/gitignore: A collection of useful .gitignore templates](https://github.com/github/gitignore)
- ![](https://www.google.com/s2/favicons?domain=www.slideshare.net) [Git 101: Git and GitHub for Beginners](https://www.slideshare.net/HubSpot/git-101-git-and-github-for-beginners)    
- ![](https://www.google.com/s2/favicons?domain=speakerdeck.com) [Git - How to unfuck // Speaker Deck](https://speakerdeck.com/mgapatrick/git-how-to-unfuck)
    - ![](https://www.google.com/s2/favicons?domain=gist.github.com) [custom bash prompt](https://gist.github.com/mgapatrick/8af91f342a2ab2ba940467bd693404b1) 
- ![](https://www.google.com/s2/favicons?domain=www.lynda.com) [Git Essential Training](https://www.lynda.com/Git-tutorials/Git-Essential-Training/100222-2.html)
