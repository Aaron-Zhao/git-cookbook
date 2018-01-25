
# Git Cookbook

> A repository for commonly used git commands.

#### Git config edit, global, local, list, caching pwd

```sh
$ git config --global -e
```
```sh
$ git config --global user.name "User Name"

$ git config --global user.email "user_email@domain.com"
```
```sh
$ git config user.name "User Name"

$ git config user.email "user_email@domain.com"
```
```sh
$ git config -l
```
```sh
# Windows
$ git config --global credential.helper wincred
# Mac
$ git config --global credential.helper osxkeychain
# Linux
$ git config --global credential.helper cache
```

#### Initializing

```sh
$ git init
```

#### Adding a remote source

```sh
$ git remote add <aliasName> <remoteAddress>
$ git remote add origin "git@github.com:Aaron-Zhao/git-cookbook.git"
```


#### Create a branch

```sh
$ git branch <newBranchName>
```

#### Checkout a branch

```sh
$ git checkout <branchName>
```

#### Create a branch and check it out right after that

```sh
$ git checkout -b <newBranchName>
```

#### Checkout a remote branch

```sh
$ git fetch
$ git checkout <branchName>
```

#### Rename a branch

```sh
$ git branch -m <newBranchName>
$ git branch -m <oldBranchName> <newBranchName>
```

#### Rename a remote branch

```sh
# rename locally
$ git branch -m <oldBranchName> <newBranchName>
# delete old remote branch
$ git push <remote> :<oldBranchName>
# push new branch to remote
$ git push <remote> <newBranchName>
```

#### Show branches

```sh
$ git branch
```

#### Adding a file and commit with comment

```sh
$ git add <file>
$ git commit -m 'Your comment'
```

#### Adding modified files and commit with comment

```sh
$ git add .
$ git commit -m 'Your comment'
```
##### above can be shorthanded with just

```sh
$ git commit -am 'Your comment'
```

#### Adding all (modified and new) files and commit with comment

```sh
$ git add --all
$ git commit -m 'Your comment'
```
#### Amending previous commit comment

```sh
$ git commit --amend -m 'New commit message'
```

#### Checking status

```sh
$ git status
```

#### Push your branch to remote

```sh
$ git push <remoteAliasName> <localBranchName>
```

#### .gitignore

```sh
# To remove all ignored but staged files
git rm -r --cached .
git add .
git commit -m "Removing all files in .gitignore"
```

Ignoring files (not to be checked in git), refer to [this docs](https://git-scm.com/docs/gitignore) for more details.

---

#### Undo

```sh
# To UNDO local unstaged file changes only (for tracked files)
$ git checkout .

# To UNDO a local unstaged file changes
$ git checkout -- <file>

# To UNDO staged file changes or new files only
$ git reset .
$ git reset <file>
$ git rm --cached <file>
$ git rm -r --cached <folder>

# To UNDO local file changes (stage or unstaged) but NOT REMOVE your last commit, then use
$ git reset --hard

# To UNDO local file changes AND REMOVE your last commit, then use
$ git reset --hard HEAD~

# To KEEP local file changes and REMOVE ONLY your last commit, then use
$ git reset --soft HEAD~

# undo x number of commits
$ git reset HEAD~<x>

# push undo to remote
$ git revert HEAD

# remove untracked files
# to see what files will be deleted
$ git clean -n

# delete untracked files
$ git clean -f

# delete directories
$ git clean -fd

# delete ignored files
$ git clean -fX

# delete ignored and non-ignored files
$ git clean -fx

```

#### Revert

```sh
# This create a new commit that reverts all changes made by <commit>
$ git revert <commit>
```

#### Working with remote

```sh
# list
$ git remote
$ git ls-remote

# verbose
$ git remote -v

# add a new remote repository of your project
$ git remote add <aliasName> <remoteAddress>

# removing an existing remote alias
$ git remote rm <aliasName>

# rename remote alias
$ git remote rename <oldAliasName> <newAliasName>

# update an existing remote URL
$ git remote set-url <aliasName> <NewRemoteAddress>

# clean up remote branches in local
$ git remote prune origin

# test without doing it
$ git remote prune origin --dry-run

# push your new branch to a remote repository
$ git push <aliasName> <branchName>

# pull a remote branch 
$ git pull <aliasName> <branchName>

# download new branches and data from a remote repository
$ git fetch <aliasName>

# merge alias to your branch
$ git merge [aliasName/branchName]
```

#### Working with branches

```sh
# show local, [remote], [all] branches
$ git branch [-r] [-a]

# create and checkout a branch
$ git checkout -b <branchName>

# rename
$ git branch -m <branchName> <newBranchName>

# get back deleted branch before it gets clean up (30 days after deletion)
$ git reflog
$ git branch <newBranchName> <deletedBranchId>

# switching between 2 branches
$ git checkout -

# delete branch with possible error message
$ git branch -d <branchName>

# delete branch without questioning
$ git branch -D <branchName>

# push local branch to remote
$ git push <remote> <branchName>

# force push local branch to remote, if you're the only one working on the branch
$ git push -f <remote> <branchName>

# force with lease otherwise
$ git push --force-with-lease <remote> <branchName>

# pull remote branch to local
$ git pull origin <branchName>

# list branches merged
$ git branch -a --merged

# list branches not merged
$ git branch -a --no-merged

# merge a branch
$ git merge <branchName>

# merge a branch with message
$ git merge <branchName> -m "Your merge message"

# rebase onto a branch
$ git rebase <branchName>

# squash x number of commits into one, follow the instructions to complete it
$ git rebase -i HEAD~<x>

# do if you want update the timestamp after squashing
$ git commit --amend --date="now"

# abort
$ git rebase --abort
$ git merge --abort

# show files in conflicts
$ git diff --name-only --diff-filter=U
# add it to an alias so you can reuse it
$ git config --global alias.conflicts "diff --name-only --diff-filter=U"
$ git conflicts

# to resolve rebase conflicts, first resolve any code conflicts by either accepting their or your changes
# then add those files to staging, you can see them by $ git status
$ git add .
# after that continue rebasing
$ git rebase --continue
# if all you code changes are replaced by their changes, skip rebase and apply your changes manually
$ git rebase --skip
# update remote with
# force push local branch to remote, only if you're the only one working on the branch
$ git push -f <remote> <branchName>
# force with lease otherwise
$ git push --force-with-lease <remote> <branchName>

# revert rebase
# reference log
$ git reflog
# reset to the place right before your rebase
$ git reset --hard HEAD@{x}
```

#### Cherry Pick

```sh
$ git cherry-pick <commit>
```

For advanced cherry-pick refer to [this docs](https://git-scm.com/docs/git-cherry-pick) for more details.

#### Tags

```sh
# list
$ git tag

# regex
$ git tag -l "v1.8.5*"

# create
$ git tag <tagName>
$ git push <remoteAlias> <tagName>

# create annotated
$ git tag -a v1.4 -m "my version 1.4"

# create and attach to a specific commit
$ git tag -a <tagName> <commitId>

# push a tag
$ git push <remoteAlias> <tagName>

# push all tags
$ git push <remoteAlias> --tags

# check a branch at a tag
$ git checkout -b <branchName> <tagName>

# reset to tag
$ git tag BACKUP
$ git reset --hard BACKUP

# delete local tag
$ git tag -d TAG

# delete remote tag
$ git push --delete origin TAG
```

#### Logs

```sh
# show commits, press 'q' to quit
$ git log 

# show commits one line
$ git log --oneline

# search
$ git log -S "search string"

# count commits
$ git log --oneline | wc -l

# commit graph
$ git log --oneline --graph

# count commits by committers
$ git shortlog -s
$ git shortlog -sne

# commits by an author
$ git log --author "Author Name"

# commits by author and search string
$ git log --grep "search string" --author "Author Name"

# commits by time
$ git log --after="2014-02-12T16:36:00-07:00"
$ git log --before="2014-02-12T16:36:00-07:00"
$ git log --until="2014-02-12"
$ git log --since="yesterday"
$ git log --since="1 month ago"
$ git log --since="2 weeks 3 days 2 hours 30 minutes 59 seconds ago"
```

#### Stashing

```sh
# stash changes
$ git stash
$ git stash save "message"

# list
$ git stash list

# show changes
$ git stash show -p

# apply
$ git stash apply
$ git stash apply stash@{stash_number}

# drop
$ git stash drop

# apply and drop
$ git stash pop
$ git stash pop stash@{stash_number}

# apply stash to a new branch
$ git stash branch
$ git stash branch <branch> <stash>
```


#### Git diff

```sh
# file diff
$ git diff <file>
$ git diff --cached <file>

# commit diff
$ git show <commit>

# show all changes in staged
$ git diff --cached

# list of files to be pushed
$ git diff --stat <remote/branch>
$ git diff --stat origin/master

# code diff of the files to be pushed
$ git diff <remote/branch>

# full file paths of the files that will change, run:
$ git diff --numstat <remote/branch>

# compare branches
$ git diff <branch_1> <branch_2>
$ gitk <branch_1> <branch_2>
```

#### Git grep

```sh
# search content in commits
$ git grep -n 'search string'

# return x number of lines before and after of the matches
$ git grep -n -C<x> 'search string'

# only "before"
$ git grep -n -B<x> 'search string'

# only "after"
$ git grep -n -A<x> 'search string'
```

#### Git blame

```sh
# show code changes line by line, with authors
$ git blame [file]
$ git blame [file] -l
$ git blame [file] -l > file_change_log.txt
```

#### Other
git ssh config file
```sh
C:\Program Files\Git\etc\ssh\ssh_config
```