# Git - GitHub
### Overview (Index)

1. [Your Config Settings](#your-config-settings)  
2. [Clone & Status](#clone--status)  
3. [Add & Commit](#add--commit)  
4. [Push Command](#push-command)  
5. [Init Command](#init-command)  
6. [Workflow](#workflow)  
7. [Git Branches](#git-branches)  
8. [Branch Commands](#branch-commands)  
9. [Merging Code](#merging-code)  
10. [Pull Command](#pull-command)  
11. [Resolving Merge Conflicts](#resolving-merge-conflicts)  
12. [Undoing Changes](#undoing-changes)  
    - [Case 1: Staged Changes](#case-1-staged-changes)  
    - [Case 2: Committed Changes (One Commit)](#case-2-committed-changesfor-one-commit)  
    - [Case 3: Committed Changes (Many Commits)](#case-3-committed-changesfor-many-commits)  
13. [Fork](#fork)
14. [References](#references)
## Your config settings
Github has a lot of settings that you can change. You can change your username, email, and other settings. Whenever you checkpoint your changes, git will add some information about your such as your username and email to the commit. There is a git config file that stores all the settings that you have changed. You can make settings like what editor you would like to use etc. There are some global settings and some repository specific settings.

Let’s setup your email and username in this config file. I would recommend you to create an account on github and then use the email and username that you have created.
```
git config --global user.email "your-email@example.com"
git config --global user.name "Your Name"
```
Now we can check your config settings:
```
git config --list --global
```
## Clone & Status

Clone - Cloning repository on our local machine

     git clone  <- some link -> 

Status - displays the state of the code

    git status
untracked - new files that git doesn't yet track <br>
modified - changed <br>
staged - file is ready to be committed <br>
unmodified - unchanged

## Add & Commit

add - adds new or changed files in your working directory to the Git staging area.

    git add <- file name->

commit- it is record of change 

    git commit -m "some message"

## Push Command 
push - upload local repo content to remote repo

    git push origin branch_name 
    git branch // for show the branch name


## Init Command 
init - used to create a new git repo

```
git init
git remote add origin <-link->
git remote -v (to verift remote)
git branch (to check branch)
git branch -M main (to rename branch)
git push origin main
```
- `git init` - used to create a new git repo
- `git remote add origin <link>`
   Connects your local project to a remote repository so you can upload (push) your code to it. Replace <link> with the URL of your remote repository.
- `git remote -v`
   Verifies the remote repository links.
- `git branch`
   Lists all the branches in your repository.
- `git branch -M main`
   Renames the current branch to 'main'.
- `git push origin main`
   Pushes your code to the 'main' branch of the remote repository.


The -u flag in git push -u origin main sets a link between your local branch (main) and the remote branch. After this, you can just use git push or git pull without typing the branch name every time.

```
git push -u origin main (now you can only write)
git push 
```

### Force Push (If You’re Sure About Overwriting)
If you’re certain your local changes should overwrite the remote branch, you can force push:
```
git push origin main --force
```
**⚠️ Warning**: This will overwrite the remote branch and discard any remote changes. Use this only if you're sure the remote changes aren't needed.


## Workflow
![github Terminology](<img/github Terminology.jpg>)

##  
![Git Branches](<img/Git-Branches.webp>)

## Branch Commands
```
git branch (to check branch)
git branch -M main (to rename branch)
git checkout <-branch name-> (to navigate)
git checkout -b <-new branch name-> (to create new branch)
git branch -d <-branch name-> (to delete branch)

```

- `git branch` - This command lists all the branches in the current repository.
- `git branch -M main` - This command renames the current branch to `main`.
- `git checkout <branch name>` - This command switches to the specified branch.
- `git checkout -b <new branch name>` - This command creates a new branch and immediately switches to it.
- `git branch -d <branch name>` - This command deletes the specified branch (only if it’s fully merged).

## Merging Code
```
git diff <branch name>
git merge <branch name>
```
- `git diff <branch name>` - This command compares commits, branches, files, and more.
- `git merge <branch name>` - This command merges the specified branch into the current branch.

## Pull Command

- `git pull origin main` used to fetch and dowload content from a remote repo and immediately update the local repo to match that content.

## Resolving Merge Conflicts
- When a conflict occurs during a merge, Git will pause and mark the conflicting files.
- Open the conflicting files, locate the conflict markers (<<<<<<, ======, >>>>>>), and decide which changes to keep.
- Edit the file to resolve the conflict and remove the markers.<br>

Once resolved, use:
```
git add <file>
git commit
```
to finalize the merge.


## Undoing Changes

```
git log 
```
`git log` - This command shows the commit history for the current branch.

### Case 1: staged changes
```
git reset <-file name->
git reset
```
`git reset <file-name>`:
This unstages a specific file, moving it from the staging area back to the working directory. The changes remain in your files but are no longer marked for commit.<br>
`git reset`:
This unstages all files in the staging area without altering the actual file changes in the working directory.

### Case 2: commited changes(for one commit)
```
git reset HEAD-1
```

`git reset HEAD-1` undoes the last commit, keeping its changes unstaged for further edits or recommit.

### Case 3 commited changes(for many commits)
```
git reset <-commit hash->
git reset --hard <-commit hash->
```
`git reset <commit-hash>:`
Takes your project back to a specific commit. The changes made after that commit are kept in your files but are removed from staging.

`git reset --hard <commit-hash>:`
Completely resets your project to a specific commit, erasing all changes made after that commit from both files and staging.

⚠️ Use --hard carefully, as it deletes changes permanently!

## Fork
A fork is a copy of a repository that you create in your own account, typically on platforms like GitHub or GitLab. It allows you to:

- Experiment and make changes without affecting the original repository.
- Submit your changes back to the original project via a pull request.

Forks are commonly used for contributing to open-source projects or developing features independently.

## References
- https://youtu.be/Ez8F0nW6S-w?si=TayaST7-nchy-pHI
- https://docs.chaicode.com/git-and-github/