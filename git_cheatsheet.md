# Git Commands

## Documentation

[Link to Git Documentation](https://git-scm.com/docs "Docs on official git documentation page")

## Git & Github Bootcamp

### Basics

Get current version

    git --version

Set git Username & Email

    git config --global user.name "my_username"
    git config --global user.email "my@email.com"

Check current Username & Email

    git config user.name
    git config user.email

Git status (also check, if you are already in a repo before initializing)

    git status

Git logging  (end log with "Q")

    git log
    git log --oneline

Initializing repository

    git init

Adding changes (each file or all)

    git add <filename> <filename>
    git add .

Committing changes

    git commit -m "commit interpretation in present tense"
    git commit -a -m "commit interpretation including adding all changes"


Amending Commits (only to last commit)

    git commit -m "some commit"
    git add <forgotten files>
    git commit --amend

### Branches

Creating a branch (or creating branch and switch to branch)

    git branch <branchname>
    git switch -c <branchname>

Get a list of all existing branches

    git branch


### Merging Branches

Fast forward merge (e.g. merge into unchanged main branch)

get onto main branch and merge other branch into main

    git merge <branchname>

Deleting branches

    git branch -d <branchname>

Force deleting branches    

    git branch -D <branchname>

### Comparing changes

Comparing staging area and working directory

    git diff
    git diff HEAD

Comparing specific files 

    git diff HEAD <filename>

Comparing two branches

    git diff branch1..branch2

Comparing two commits

    git diff commit1..commit2

### Reversing 

Checkout to older commit (result in detached HEAD)

    git checkout <commit id from log>

Get back to last branch with 

    git switch -

While in detached HEAD, create new branch and switch to it

    git switch -c <new-branch-name>
    git add . 
    git commit -m "new branch with stuff from older version"
    git switch master

Discarding changes in file 

    git checkout HEAD <filename>

Discarding changes after last commit

    git restore <filename>

Unstaging 

    git restore --staged <filename>

Undo commits (delete commits but not progress in file, e.g if you want progress on another branch)

    git reset <commit id>

Undo commits AND all changes since this commit

    git reset --hard <commit id>

Undo commits and create a new branch (better within collaborating teams)

    git revert <commit id>


## Github

### Cloning repositories

    git clone <github-url>

### Connect to Github (from existing local repo )

    git remote add origin <"github-url">
    git remote -v
    git push origin <branchname>
    git push -u origin <branchname>


1. Create new repository in Github
2. connect local repo to Github repo
3. check, if orign equals remote github url
4. push to remote repository
5. (alternative to 4) push to remote repo and setup upstream to default
6. before pushing stuff up, always pull down to see, if there are changes

### Working with remote branches

After cloning the repo, i only see main (or master) branch locally
To swith to remote branch origin/puppies => remote is usually called "origin"

    git switch puppies

To see remote branches

    git branch -r

### Fetching from remote

To fetch into local repository BUT not into working directory:

    git fetch
    git fetch <remote>
    git fetch <remote> <branch>

To look at those changes, checkout to remote master branch like:

    git checkout origin/master

### Pulling from remote

To get changes from remote and integrate them into local working directory. It update the branch, that you are currently on (e.g. being on master will update master branch)

    git pull
    git pull <remote> <branch>

Pulls can result in conflicts - just resolve them and than add, commit and push changes.


