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

### Merge Conflicts

Sometimes when trying to merge a branch into another branch or into main:

```bash
error: Merging is not possible because you have unmerged files.
hint: Fix them up in the work tree, and then use 'git add/rm <file>'
hint: as appropriate to mark resolution and make a commit.
fatal: Exiting because of an unresolved conflict.
```

We can use: `git status` to check the merge conflicts

```bash
On branch CRU-97-Frontend-App-Design
Your branch is ahead of 'origin/CRU-97-Frontend-App-Design' by 4 commits.
  (use "git push" to publish your local commits)

You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Changes to be committed:
        modified:   api/Dockerfile
        new file:   api/src/app/models.py
        new file:   api/src/app/views/docker_api.py


Unmerged paths:
  (use "git add/rm <file>..." as appropriate to mark resolution)
        both modified:   api/src/app/__init__.py
        deleted by them: api/src/app/api.py
        both modified:   api/src/test/test_docker_api.py

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        deleted:    api/src/app/templates/404.html
        deleted:    databaseSetup.sh
```

We can now clean up
`git add <file>`: To add a file from the remote repository
`git rm <file>`: Removing a file from the remote repository

> _Note_: If you're already in conflicted state, and you want to just accept all of theirs:

```
git checkout --theirs .
git add .
```

If you want to do the opposite:

```
git checkout --ours .
git add .
```

## Fork a repository

A fork is basically a clone of a project repository that is completely independent from its original remote / local repository and future commits are pushed to the new repository other than the old one.

Forking a repository is usually done via the github UI, due to the fact that from git’s perspective, a fork is just another clone of the repository that is now uploaded into a different location ( something other than origin) which is tracked by githubs databases

Making a fork
`git clone https://github.com/YOUR-USERNAME/Spoon-Knife`
