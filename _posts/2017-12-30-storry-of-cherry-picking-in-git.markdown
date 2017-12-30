---
layout: post
comments: true
title:  "Storry of cherry-picking in git"
date:   2017-12-30 18:19:50 +0545
categories: blog
---

Git is a strong version control tool that had made my programming life much easier to manage. Specially when programming with groups of people.

Me and my friend were working on same project one day. We were working on two different branch with same base branch.
I committed my changes in my branch and he committed his changes in his. While I was working on my branch I came across a bug. I looked into it and made changes to fix it. I committed the changes and pushed to origin.

Later I found out that the bug was present in the base branch and since the branch my friend was working on was branched off from same base branch, his branch also contains the same bug. When he found the bug he came to me and asked about the bug and ways to fix it. I told him that I have already fixed it in my branch and did a push to github.

Since the bug was hindering his progress, he needed the fix before going any further. The possible options for him were:
> Write the bugfix and commit to his branch (which is redundant and could cause conflicts when we merge both our branch to the base branch)
> Wait for my branch to be merged to the base branch and rebase the base branch to his branch (This would take too long as my branch was not ready to be merged to the base branch)

There was also a third option, '*cherry-pick*'. It was the best options we had. So I asked him to pull changes from github and gave him an commit id, in which I have made the bugfix. He did the pull and asked, what to do with the commit id I gave. So I gave him the command to cherry-pick my commit. The command was something like `git cherry-pick [commit-id]`. He run the command in his branch and *boom*; my bugfix commit was also available in his branch. Now he could move forward with his changes without worrying about the bug.
