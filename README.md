---
languages: html, css
tags: git, todo
resources: 1
---
# Git Merge Conflicts

![What Did I Tell You](http://www.wired.com/images_blogs/underwire/2009/11/80s_movies_14a.jpg)

## Introduction

Marty McFly just finished his student profile and now needs to merge his profile with Doc Brown's so they'll both be on the student index page.

## Merging Git Branches

Marty's profile is stored in the `master` branch. Doc's is in the `doc-brown` branch. We are merge both branches onto a new branch and resolve the merge conflits there befor putting it all back on the master branch.

### Step 1: Make sure you have both branches

Make sure you are in the `master` branch.
- run `git branch` in the terminal, while you're in the "git-merge-conflicts folder"

The output should look like this:

```bash
$ git branch
* master
  doc-brown
```

If you do not see the `doc-brown` branch, you will need to fetch it.
- run `git fetch origin/doc-brown`

Now you're output should include both branches. (run `git-branch` again to check. If you don't have both branches, grab an instructor or ask a teammate for help.


### Step 2: Make a new merge branch

Create a new branch using `git checkout -b <new branch name>`
- run `git checkout -b merge-index-pages`

You should now be in the `merge-index-pages` branch.
 _(Remember: you can check by running `git branch`)_

 ### Step 3: Merge!

 From the `merge-index-pages` branch merge the branches `git merge <branch name>`
 - run `git merge master`

 But wait!!! There's a merge conflict!

 ```bash
 a bunch of stuff about the merge conflict
 ```

 ### Step 4: Fix the conflicts
