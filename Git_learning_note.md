# Pro Git

## Getting started

* The Three States: three main states that your files can reside in - modified, staged, and committed
	* **Modified** means that you have changed the file but have not committed it to your database yet. 
	* **Staged** means that you have marked a modified file in its current version to go into your next commit snapshot. 
	* **Committed** means that the data is safely stored in your local database.
* Three main sections of a Git project: the working tree, the staging area, and the Git directory.
	* The working tree is the place to work on the files
	* The staging area is the place to store the modified files to commit.
	* The Git directory is the place to store the committed files.
* The basic Git workflow: 
	1. You modify files in your working tree. 
	2. You selectively stage just those changes you want to be part of your next commit, which adds only those changes to the staging area. 
	3. You do a commit, which takes the files as they are in the staging area and stores that snapshot permanently to your Git directory.

### First-Time Git Setup

```
$ git config --list
$ git config --list --show-origin
```

### Getting help

```
$ git help <verb>
$ git <verb> --help
$ man git-<verb>
$ git <verb> -h //concise help
```

## Git Basics
File status:
untracked, unmodified, modified, staged

In the simple case, a repository might have a single .gitignore file in its root directory, which applies recursively to the entire repository. However, it is also possible to have additional .gitignore files in subdirectories. The rules in these nested .gitignore files apply only to the files under the directory where they are located.

To see what you’ve changed but not yet staged, type git diff with no other arguments. If you want to see what you’ve staged that will go into your next commit, you can use git diff --staged. This command compares your staged changes to your last commit.

Every time you perform a commit, you’re recording a snapshot of your project that you can revert to or compare to later.


```
$ git init
$ git add *.c
$ git commit -m 'initial project version'

$ git clone https://github.com/libgit2/libgit2
$ git clone https://github.com/libgit2/libgit2 mylibgit

$ git status
$ git status -s

$ git diff
$ git diff --staged
$ git diff --cached

$ git commit
$ git commit -m "Some descriptions"
$ git commit -a -m "Add and commit"

$ git rm test.txt
$ git rm --cached test.txt

$ git mv test test.txt

$ git log
$ git log --pretty=oneline

$ git commit --amend

$ git reset HEAD <file>

$ git checkout -- <file>

$ git remote -v

$ git remote add <shortname> <url>

$ git fetch <shortname>

$ git fetch origin

$ git pull

$ git push <remote> <branch>

$ git remote show <remote>

$ git remote rename <newname> <oldname>

$ git remote remove <remote>

$ git remote rm <remote>

$ git tag

$ git tag [--list | -l] <"patterns">

$ git tag -a <tag> -m "message"

$ git tag -a <tag> <short id> -m "message"

$ git show <tag>

$ git tag <tag> #似乎跟git tag -a没有差别 2.16.1

$ git tag -d <tag>

$ git push <remote> <tagname>

$ git push <remote> --delete <tagname>

$ git checkout -b <branch> <tag>

$ git config --global alias.unstage 'reset HEAD --'

$ git config --global alias.last 'log -1 HEAD'
```

## GIT BRANCHING

```
$ git branch <branchname>
$ git log --online # git log --online跟git log --online --decorate相同
$ git checkout <branchname>
$ git checkout -b <newbranchname>
$ git branch -d <branchname>



```


## Resource
[.gitignore examples](https://github.com/github/gitignore)