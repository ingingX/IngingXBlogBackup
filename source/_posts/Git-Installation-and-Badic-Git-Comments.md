---
title: Start with Git
date: 2020-02-25 15:23:30
tags: Git
category: Tech Skills
---

Topics: Git Installation and Basic Git Comments.

[Git](https://git-scm.com/) is a free and open source distributed version control system. We can use it to operate our [GitHub](https://www.github.com) repos. Now let's see its installation and some basic comments!

## Part 1: Git Installation (for Windows)

### 1. Download 'git.exe'

Click [here](https://git-scm.com/download/win) and download the right version.

You may need some proxy to accelerate the downloading process.

### 2. Click 'next'

Open your '.exe' file just downloaded, and click 'next' for default installation, or choose 'custom install' if you know what you are doing.

### 3. Now it's all set! Try out your first Git Comment! 

See Part 2 below! 

## Part 2: Basic Git Comments

### 1. Git Architecture

![](/image/gitComments.png)

### 2. Basic Git Comments

``` bash
# initial current folder
$ git init 

# clone / dowmload a repo
$ git clone [url] [givenDir]

# show Git Configure File
$ git cinfig -l 

# set Username and Password
$ git config --global user.name "yourUsername"
$ git config --global user.email "yourEmail"
$ git config --global user.password "yourPassword"

# add file from 'givenDir' to 'Index'
$ git add [givenDir]

# add file from 'currentDir' to 'Index'
$ git add .

# rename and add file to 'Index'
$ git mv [file-original] [file-renamed]

# submit 'Index' to 'Repo'
$ git commit -m [message]

# submit 'Workspace' to 'Repo'
$ git commit -a

# show file changes
$ git status

# show current-branch changes
$ git log

# show difference between 'Workspace' and 'Index'
$ git diff

# show all the 'Remote' Repos' info
$ git remote -v

# show ONE 'Remote' Repo's info
$ git remote show [remote]

# fetch all 'Remote' Repos and merge into 'Workspace'
$ git fetch [remote]

# fetch 'Remote' changes, and merge to local branches
$ git pull [remote] [branch]

# push all 'Repos' to 'Remote'
$ git push [remote] --all

# push current 'Repo' to 'Remote', ignoring conflict
$ git push [remote] --force

# release a downloadable archive file
$ git archive
```

### 3. Some words

Of course, this article is just a small glance of Git. As referred in the beginning, Git is a powerful tool. You can read [official documents](https://git-scm.com/docs) for more detailed and advanced usage. 

And at the same time, I will keep this article updated along with my journey of coding and studying.