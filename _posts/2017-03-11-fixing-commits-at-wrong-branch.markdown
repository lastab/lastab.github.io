---
layout: post
title:  "Git (Fixing Commits At Wrong Branch)"
date:   2017-03-11 18:19:50 +0545
categories: blog
meta_keywords: git-and-me git-experience git-firsttime
meta_description: git and me
---

There are great chances of making mistakes while committing our changes in git. One of the common mistake that we might make is that we might commit in wrong branch.
While working with different branches in a project, there is a chance that we might commit in wrong branch. This can cause lots of effort and time to fix them manually one by one, especially when there are commits for lots of changes.
But thankfully it is git that we are talking about. There are different ways to fix this problem. Each has their own advantages and disadvantages. I am going to talk about one of the best one.

_Step1:_

  Checkout to the branch where you have the commits that needs to be moved.
  
  {% highlight bash %}
  git checkout <wrong-branch>{% endhighlight %}
  
_Step2:_

  Note the commit's hash(or initial hash and final hash if all commits are that needs to be moved to the correct branch)
  
  {% highlight bash %}
  git log --oneline{% endhighlight %}
  
  {% highlight bash %}
d81b02b commit3 for right-branch
3d8b005 commit2 for right-branch
4d31325 commit1 for right-branch
b4f411c commit for wrong-branch
{% endhighlight %}
  
_Step3:_

  Use hard reset to get the current branch to the initial state
  
  {% highlight bash %}
  git reset --hard b4f411c #git reset --hard <hash>{% endhighlight %}

_Step4:_

  Checkout to the correct branch where the commits needs to be moved
   {% highlight bash %}
  git checkout <right-branch>{% endhighlight %}

_Step5:_

  if single commit needs to be added:
  {% highlight bash %}
  git cherry-pick 4d31325 #git cherry-pick <hash>{% endhighlight %}

  if multiple continous commits needs to be added:
  {% highlight bash %}
  git cherry-pick 4d31325...d81b02b #git cherry-pick <inital-hash>...<final-hash> {% endhighlight %}

And you are done. The commit(s) will now be in correct branch. 

This method is one the best one as this method does not require rewriting commit message(s). But the hash value(s) must me remembered for this method.
