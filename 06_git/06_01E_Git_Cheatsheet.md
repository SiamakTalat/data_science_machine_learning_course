# Git Cheatsheet
**Python for Data Science and Machine Learning Bootcamp — Sections 50A–50D**

---

## Setup & Configuration
```bash
git --version                          # confirm Git is installed
git config --global user.name "Name"   # set your name (once)
git config --global user.email "a@b"   # set your email (once)
git config --global init.defaultBranch main
git config --global core.editor "code --wait"
git config --list                      # view all settings
```

---

## Starting a Repository
```bash
git init                               # turn current folder into a repo
git clone <url>                        # copy a remote repo locally
git clone <url> my-folder              # clone into a custom folder name
```

---

## Daily Basics — Status, Stage, Commit
```bash
git status                             # what changed since last commit
git status -s                          # compact one-line format
git diff                               # unstaged changes (working tree vs staging)
git diff --staged                      # staged changes (staging vs last commit)

git add <file>                         # stage a specific file
git add .                              # stage all changes
git add *.py                           # stage all .py files
git add -p <file>                      # stage individual hunks interactively

git commit -m "message"                # commit staged changes
git commit -am "message"               # stage tracked files + commit in one step
git commit --amend                     # edit last commit (message or content)
```

---

## Viewing History
```bash
git log                                # full commit history
git log --oneline                      # one line per commit
git log --oneline --graph --all        # visual branch graph
git log -5                             # last 5 commits only
git log --author="Alice"               # filter by author
git log --grep="fix"                   # filter by message keyword
git log -S "function_name"             # commits that added/removed a string
git log --oneline -- analysis.py       # commits that touched a specific file
git show HEAD~1                        # inspect the previous commit
```

---

## Undoing Changes
```bash
git restore <file>                     # discard edits in working tree
git restore --staged <file>            # un-stage (keep edits)
git restore --source=HEAD~2 <file>     # restore file to a past commit's state

git reset --soft HEAD~1                # un-commit, keep changes staged
git reset --mixed HEAD~1               # un-commit, un-stage (default)
git reset --hard HEAD~1                # un-commit + discard changes (destructive)

git revert <sha>                       # safe undo — creates a new reversal commit
```

> `git revert` is safe on shared branches. `git reset` only on local unpushed commits.

---

## Branching
```bash
git branch                             # list local branches (* = current)
git branch -v                          # list with last commit message
git branch -a                          # list local + remote branches
git branch --merged main               # branches already merged into main

git switch -c feature/name             # create + switch to new branch
git switch main                        # switch to existing branch
git switch -                           # switch to previous branch

git branch -m new-name                 # rename current branch
git branch -d feature/name             # delete merged branch (safe)
git branch -D feature/name             # force delete unmerged branch
```

---

## Merging
```bash
git merge feature/name                 # merge branch into current branch
git merge --no-ff feature/name         # force a merge commit (no fast-forward)
git merge --abort                      # cancel an in-progress conflicted merge
```

**Resolving a conflict:**
1. Open the conflicted file — edit away the `<<<<<<<`, `=======`, `>>>>>>>` markers
2. `git add <file>`
3. `git commit`

---

## Remotes
```bash
git remote -v                          # list remotes with URLs
git remote add origin <url>            # add a remote named origin
git remote set-url origin <url>        # change a remote's URL
git remote rename origin backup        # rename a remote
git remote remove origin               # remove a remote
git remote show origin                 # inspect remote details
```

---

## Fetch, Pull, Push
```bash
git fetch origin                       # download changes — does NOT touch local files
git diff main origin/main              # compare local vs remote after fetch

git pull                               # fetch + merge into current branch
git pull --rebase                      # fetch + rebase (cleaner history)

git push                               # push current branch to its tracked remote
git push -u origin feature/name        # first push of a new branch (sets tracking)
git push --tags                        # push all tags
git push origin --delete feature/name  # delete a remote branch
```

---

## Tracking Branches
```bash
git branch -vv                         # show ahead/behind counts for each branch
git branch --set-upstream-to=origin/main main
git switch --track origin/feature/eda  # create local branch tracking a remote one
```

---

## Stashing
```bash
git stash                              # shelve current changes
git stash push -m "description"        # stash with a label
git stash push --include-untracked     # include new untracked files

git stash list                         # show all stashes
git stash pop                          # apply + remove most recent stash
git stash apply stash@{1}              # apply a specific stash (keeps it in list)
git stash drop stash@{0}               # remove a stash without applying
git stash clear                        # remove all stashes
```

---

## Tagging
```bash
git tag                                # list all tags
git tag v1.0                           # lightweight tag on current commit
git tag -a v1.0 -m "First release"     # annotated tag (preferred)
git tag -a v0.9 <sha> -m "Beta"        # tag a past commit
git show v1.0                          # inspect tag details
git push origin v1.0                   # push a single tag
git push --tags                        # push all tags
git tag -d v1.0                        # delete tag locally
git push origin --delete v1.0          # delete tag on remote
```

---

## Rebasing
```bash
git rebase main                        # rebase current branch onto main
git rebase -i HEAD~3                   # interactive rebase — last 3 commits
git rebase --continue                  # after resolving a conflict
git rebase --abort                     # cancel rebase
```

**Interactive rebase options:** `pick` · `reword` · `squash` · `fixup` · `drop`

> Never rebase commits already pushed to a shared branch.

---

## Cherry-pick & Bisect
```bash
git cherry-pick <sha>                  # apply one commit to current branch
git cherry-pick --no-commit <sha>      # apply changes without committing

git bisect start                       # begin binary search for a bug
git bisect bad                         # mark current commit as broken
git bisect good v1.0                   # mark a known good commit
git bisect reset                       # end bisect, return to HEAD
```

---

## .gitignore
```bash
git check-ignore -v <file>             # why is this file ignored?
git status --ignored                   # list all ignored files
git rm --cached <file>                 # stop tracking a committed file
```

**Common patterns:**
```
__pycache__/      *.pyc        .ipynb_checkpoints/
.env              *.csv        *.pkl        models/
.venv/            .DS_Store    .vscode/
```

---

## Aliases (shortcuts)
```bash
git config --global alias.s   'status'
git config --global alias.lg  'log --oneline --graph --all --decorate'
git config --global alias.ll  'log --oneline -10'
git config --global alias.undo 'reset --soft HEAD~1'
git config --get-regexp alias          # view all aliases
```

---

## Fork → Clone → PR Workflow
```bash
# 1. Fork on GitHub (click Fork)
git clone https://github.com/YOU/repo.git
git remote add upstream https://github.com/ORIGINAL/repo.git

# 2. Create a branch
git switch -c feature/my-change

# 3. Work, commit, push
git add .
git commit -m "Add my change"
git push -u origin feature/my-change
# → Open Pull Request on GitHub

# 4. After PR is merged — sync your fork
git switch main
git fetch upstream
git merge upstream/main
git push origin main
git branch -d feature/my-change
```

---

## Data Science Quick Rules
| Do | Don't |
|----|-------|
| Track `.py`, `.ipynb`, `config.yaml`, `requirements.txt` | Commit large datasets (use DVC) |
| Clear notebook outputs before committing | Commit `.env` or API keys |
| Write meaningful commit messages | Force push to `main` |
| Use feature branches | Commit directly to `main` |
| Tag model-ready versions | Track `__pycache__/` or `.ipynb_checkpoints/` |

---

*Sections: **50A** Basics · **50B** Branching · **50C** Remotes · **50D** Advanced*
