---
layout: post
comments: true
title:  "Finding Files Lost In Branches"
date:   2018-02-10 18:19:50 +0545
categories: blog
---

While working with git, developing features in individual branch is a good practice. Just do
> `$ git checkout -b my-awesome-feature-branch`

and you have a new branch. This looks fun right? Whenever you want to develop a new feature, just branch off from main base branch(usually master) and start developing on it. And when your feature is ready you can merge it back to the base branch.

While working on multiple branch, it becomes hard to track what you did in each branch. It becomes more difficult to keep track of which branch contains a particular file. Searching for a file in branches is not that simple. We can not use the methods that we normally use to search files inside a folder here.

The problem can be solved manually by `checkout`ing each branch and running search command.
We can also solve it more easily by using `for loop` through each branch(available in local) and listing matched files present in each branch.
The scipt can be something like:
> ``$ for branch in `git for-each-ref --format="%(refname)" refs/heads`; do
  echo $branch :; git ls-tree -r --name-only $branch | grep '<foo>'
done``


Here ,
- `git for-each-ref --format="%(refname)" refs/heads` lists all the refname of each branches present in your local repo.
- ``for branch in `git for-each-ref --format="%(refname)" refs/heads`` does the loop and puts each refname in `$branch`
- `echo $(branch )` prints the name of branch
- `git ls-tree -r --name-only $branch` lists path to each file present in `$branch`
- `grep '<foo>'` filters the result(lists of files' path) allowing only matching filename in the list


Sample output in my project when search text is '_lost_'
``refs/heads/experience-withi3-desktop-environment :
refs/heads/finding-files-lost-in-branches :
_posts/2018-02-10-finding-files-lost-in-branches.markdown
refs/heads/gh-pages :
refs/heads/master :
refs/heads/master-bak :
refs/heads/story-of-cherry-picking :
``

The file was present in `refs/heads/finding-files-lost-in-branches` and the path was `_posts/2018-02-10-finding-files-lost-in-branches.markdown`
