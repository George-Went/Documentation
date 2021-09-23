# Git

git is a free and open sourced version control system that allows users to handle updates and changes to source code during software development. While it is primarily designed to work with programming files, it can also work with any type of text file.

## Setting up git

### Downloading Git

On linux, depending on the distribution and package manager  
ubuntu: `sudo apt install Git`  
redhat / centos: `sudo yum install Git`

### Creating a new Repository

move to the directory that you want to create
Initilise git using:  
`git init`

### Add a file to the repo

This is so that git recognises changes and saves the new repo
`touch readme.txt`  
we can chech the new files that git recognises using
`git status`

### Adding to the staging branch

This adds all new files to the repo index (.git)
`git add . `

### Commiting a file to the local repository

`git commit -m <message> `  
This commits the files to the local version of the remote repository
If you just had a local repository this would be the last step

### Creating a new remote repository

`git remote add origin <url>`  
This adds a new repository on the url
The origin is an alias for the url, so instead of calling
your remote repo an long url, you just call it "origin" (like a domain name)

`git remote`  
shows the remote repository that the local repo is linked to

### Uploading work to the remote repository

`git push origin master`  
This pushes the changes in the local remote to the remote repository
on the master branch

#### Additional Infomation

To see what your origin is:
`git remote -v`

You can also save your repositories location so you only have to type `git push`:
`git --no-pager branch -vv`
If the response has a `*` before it, it has been saved as the main repository.

## Connecting to existing repositories

### Downloading the repository

Go to the directory that you want the repo in
`git clone <remote repo url>`

### Adding to the staging branch

`git add . `  
This adds all new files to the repo index

### Commiting a file to the local repository

``git commit "message"`  
 This commits the files to the local version of the remote repository
If you just had a local repository this would be the last step

### Pushing files to the remote repository

`git push origin master`  
This pushes files to the origin repo on the master branch

### Pulling new files from the remote repo

`git fetch origin`  
remember that you can just use the url as well

`Git status`  
shows the status of the git repo

## Git branches

ref: https://www.atlassian.com/git/tutorials/using-branches  
git branches are multiple versions of the same projectuseful when you want to make changes to a project that you are unsure about, or when multiple people are working on a project.

### Listing Branches

`git branch`

### Deleting a Branch

Safe delete (will not remove a branch if you have unmerged changes)  
`git branch -d <branch name>`

Force Delete  
`git branch -D <branch name>`

### Listing Remote Branches

`git branch -a`

### Creating a branch

`git branch <branch name>` (don't name the branch master)

### Moving to a branch

`git checkout <branch name>`

### Merging a branch

move to the branch you want to be merged into another
`git merge <branch>`
This can result in conflicts, so rungit add <filename>
to add the edited files to the master repo

### Renaming a branch

`git branch -m <branch>`

## Git Checkout

### Fetching remote branches

`git fetch`

### Switching to a branch

`git checkout <branch>`

## Lifecycle of a git branch

### Fast Foward Merge

This is where main does not develop on its own and new features are added to main by branchng off, then being intergrated later on.
Code is only added to main branch and conflicts are mainly to do with new functions being added.

```bash
# Start a new feature
git checkout -b new-feature main
# Edit some files
git add <file>
git commit -m "Start a feature"
# Edit some files
git add <file>
git commit -m "Finish a feature"
# Merge in the new-feature branch
git checkout main
git merge new-feature
git branch -d new-feature
```

### 3-way Merge

This is where main progresses as well as a feature branch, meaing that both `main` and `feature-branch` will conflic with each other.

```bash
# Start a new feature
git checkout -b new-feature main
# Edit some files
git add <file>
git commit -m "Start a feature"
# Edit some files
git add <file>
git commit -m "Finish a feature"
# Develop the main branch
git checkout main
# Edit some files
git add <file>
git commit -m "Make some super-stable changes to main"
# Merge in the new-feature branch
git merge new-feature
git branch -d new-feature
```

### "Merge this repository feature that I've finished" 
```bash
# stash or commit currrent changes to your own repository 
git add . 
git commit -m "commit message"
# Checkout the branch with the PR (Pull Request) 
git checkout <feature branch>
# Test that the new feature works
# Go to Bitbuket / Github and accept the feature 
# Tell the person whose PR it is that it has been accepted 
# Merge the feature into dev / main
git checkout dev
git merge <feature branch> 
# move back to your own repository 
git checkout <my branch>
```
Once Merged into dev 
```bash
# stash or commit current changes in your own branch 
git add .
git commit -m "commit message"
# checkout dev / main
git checkout dev
# pull the new changes from dev/main - this will include the new PR features that you've added to dev/main
git pull dev 
# go back to your own branch
git checkout <my branch>
# Merge dev/main into your own branch
git merge dev/main
```

## Fork a repository

A fork is basically a clone of a project repository that is completely independent from its original remote / local repository and future commits are pushed to the new repository other than the old one.

Forking a repository is usually done via the github UI, due to the fact that from git’s perspective, a fork is just another clone of the repository that is now uploaded into a different location ( something other than origin) which is tracked by githubs databases

Making a fork
`git clone https://github.com/YOUR-USERNAME/Spoon-Knife`
