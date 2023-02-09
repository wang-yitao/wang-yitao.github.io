---
layout: post
title: How to manage your github repo for your cloned website
date: 
description: 
tags: 
categories: 
---

Since I have been using [al-folio]() theme for a while and have modified a large portion of code to suit my purposes and aesthetics, it might be good to keep track of the developing process and meanwhile to keep my website up-to-date with the upstream branch to have new functionality. 

# Create a local branch for pulling from upstream

Once I had nightmare when I tried to upgrade the my repository version by directly pulling from the upstream to my master branch. I followed the instruction to rebase the repository to the newest version. However, I already had a gigantic amount of change that causes compatibility problem with the newest version and it turned out I couldn't just cancel the rebase in a clean way halfway through the process. I remember I had a really bad day and in the end I just kill my local repo and clone it once again from my github.

In the hindsight, I should really clone a local branch first that is not tied to my remote repo and thus would not affect my website even if I couldn't rebase and resolve the conflicts. So here are the step-by-step procedures:

1. Create a new branch named `update` based on the current HEAD (in my case just `master` branch)

    ```bash
    git branch update
    ```

2. Since we may want to make quite, small update on `master` for convenience and only leave `update` branch for upgrading, the `master` might be several commits ahead of the `update` so need to merge change from `master` to `update` before rebasing. 

    ```bash
    git checkout update
    git merge master
    ```

3.  