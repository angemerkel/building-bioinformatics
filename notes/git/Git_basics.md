---
editor_options: 
  markdown: 
    wrap: 72
    
title: "Git for version control"
---

# Introduction

This note book is based on the Pro Git book, written by Scott Chacon and
Ben Straub:\
<https://git-scm.com/book/en/v2>.

A cheetsheet can be found here: <https://git-scm.com/cheat-sheet>

# Git basics

## Get started

### Start a project from scratch

Using the terminal

```         
 # create a folder 
 mkdir test
 cd test
 
 # make this a local git repository 
 git init
```

Or, if you are using RStudio do:

```         
 File > create new project >  git repository
```

### Clone a remote repository to your computer

```         
 git clone <url>
```

## Stage and commit

As version control software, git tracks not only your files but also
your files as as they are (= '*file* *status'*), such as adding,
deleting and modifying a file.

**staging:** In order to track a file, git first creates an index of
each/all file/file status (aka indexing it/ them).

**commit:** Once the index of changes is created, they can then be
[recorded]{.underline} or 'commited' to the git memory.

Any change you want to be committed, needs to be staged first.

```         
 ## In your local git repository directory
 
 # stage all files 
  git add . 

 # commit with message (without -m git will open a text editor)
  git commit -m "Initial commit" 
 
 # stage and commit all changes
  git commit -am "message"
```

## Deleting or renaming files

When deleting or renaming a file you are performing a modification that
needs to be tracked:

```         
 # delete file and stage all modifications
  rm file
  add .

 # git shortcut for deleting a file
  git rm file

 # similarily git shortcut for renaming a file
  git mv file_old file_new
```

## Tracking changes

### Files status

Files can be in any of the following states:

-   untracked (never been staged); unmodified; modified; staged

```         
 # check file status
 git status
```

Examples:

-   Adding a new file or renaming a file without git mv -\> adds an
    untracked file

-   Staging changes to file (-\> modified file) and commit -\> changes
    this file into unmodified status, since all modification have been
    recorded

-   Modify a file and check again -\> you will see that the file has
    moved to status modified

### Check for differences

```         
 # show all changes (default = all unstaged changes)
 git diff
 
 # show all staged and unstaged changes
 git diff HEAD
```

\*HEAD refers to the current branch you are on (see further down for
details)

### Discard your changes

```         
 # unstage all changes to a file
 git reset file
 
 # reverse all modifications to an unstaged file
 git restore file
```

## Repositories on remote servers, e.g. on github

You may want to use a repository on a remote server, either as a backup
for your local repository or to share your repository for distribution
or collaborative development.

### Setting up a new repository on github:

1.  If you do do not have an account, create one under
    <https://github.com>

2.  Set up new repository on github <https://github.com/angemerkel> with
    a default branch called 'main' repository \> new repository \>
    private

3.  Give the remote repro a local alias, by convention the default will
    be 'origin'

4.  You can set up a communication to a local repository either via
    https (using an URL) or ssh (using an ssh-key). If you are using
    ssh, make sure you have a public-private key-pair set up.

To retrieve the URL or ssh-key, go to:\
github \> repository \> code

### Connect the remote and your local repository

\# Add a remote (URL/ssh-key) to an alias (i.e. give your remote
repository a name, 'origin' by default)
`git remote add origin [git\@github.com](mailto:git@github.com){.email}:angemerkel/Test.git`

4.  make sure your local branch is called 'main' (this is by convention
    the default) `git branch -M main`
5.  connect your remote branch to your local branch (called 'tracking')
    `git branch --set-upstream-to=origin/main main`

# Branching

### Basic operations

Create a branch:

```         
# create a branch
 git branch <name>

# create a branch at a specific reference (commit)
 git branch <name> <reference>
 
# switch to work on that branch
 git checkout <name>
 
# or short both at the same time
 git checkout -b <name> 
```

Merge a branch:

```         
# merge a branch with your current branch
 git merge <branch>
```

Reconcile branches, resolving conflicts :

git will try to reconcile the branches, and can do this in different
ways;

\- `'fast-forward'` = the commit of the second branch can be reached by
simple forwarding, i.e. simple addition or deleting changes

\- `'recursive'` = changes have to be reconciled, sometimes that will
result in conflict that need to be resolved

When performing the merge and there are conflict git will mark them (by
default via the default text editor):

```         
# <<<<<<< HEAD:index.html
# <div id="footer">contact : email.support@github.com</div>
# =======
# <div id="footer">
#  please contact us at support@github.com
# </div>
# >>>>>>> iss53:index.html

'>>>' and '<<<' indicate the diverging parts '====' indicates the separation between files
```

You will have to adjust this part and remove the indicators, than stage
the changes to show the conflict has been resolve. Once you commit, the
commit message by default will include information about the merge.

### Managing branches

```         
 # have a look at all your branches '*' indicates the branch you are currently on
 git branch 
 
 # show all branches and their last commit 
 git branch -v
 
 # show all branches that have been merged to your current branch
 git branch --merged
 
 # show all branches that not have been yet merged to your current branch
 git branch --no-merged
 
 # locally rename a branch
 git branch --move <old-branch> <new-branch>
 
 # delete a branch
 git branch -d <branch>
 
 
```

# Sync with remote repositories

You can add a remote via a reference (= alias). Reference are not the
repositories themselves but pointers to a state of a repository.

```         
 # add a remote
 git add remote <remote name> <URL/ssh-key>
```

You can get a list of all remotes and additional info

```         
 # list remotes and references
 git ls-remote
 
 # show more info on remote configuration
 git remote show <remote>
```

Fetching

Fetch retrieves updates from your remote branch. There are only pointers
not an editable local repository. In other words, fetch moves your local
pointer to match the remote state. You can review the changes and merge
them with your local branch (stage + commit)

```         
 # fetch updates (here 'origin' since it is the default alias)
 git fetch origin
```

Pushing

You can update the remote repository with your local repository

```         
# Push changes to remote branch
git push <remote> <branch>

# Example
git push origin 111

# Push local branch with a different branch name
git push origin 111:v1
```

Tracking

Pulling

# Additional resources

Other great resources to learn about git can be found on github:

**Git and github learning resources:**

<https://docs.github.com/en/get-started/start-your-journey/git-and-github-learning-resources>

A good subject specific entry point is the:

<https://learn.github.com/skills>

Highly recommended is the interactive app for learning about branching
(local & remote):

<http://learngitbranching.js.org/>

## 
