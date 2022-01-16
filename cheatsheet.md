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

Git logging

    git log
    git log --oneline

Initializing repository

    git init

Adding changes (each file or all)

    git add <filename> <filename>
    git add .

Committing changes

    git commit -m "commit message in present tense"
    git commit -a -m "commit message including adding all changes"


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





