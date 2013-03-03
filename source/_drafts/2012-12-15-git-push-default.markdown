---
layout: post
title: "Git: push.default"
date: 2012-12-15 22:00
comments: true
categories: [git]
---


push.default
Defines the action git push should take if no refspec is given on the command line, no refspec is configured in the remote, and no refspec is implied by any of the options given on the command line. Possible values are:

nothing - do not push anything.

matching - push all branches having the same name in both ends. This is for those who prepare all the branches into a publishable shape and then push them out with a single command. It is not appropriate for pushing into a repository shared by multiple users, since locally stalled branches will attempt a non-fast forward push if other users updated the branch. + This is currently the default, but Git 2.0 will change the default to simple.

upstream - push the current branch to its upstream branch. With this, git push will update the same remote ref as the one which is merged by git pull, making push and pull symmetrical. See "branch.<name>.merge" for how to configure the upstream branch.

simple - like upstream, but refuses to push if the upstream branch's name is different from the local one. This is the safest option and is well-suited for beginners. It will become the default in Git 2.0.

current - push the current branch to a branch of the same name.

The simple, current and upstream modes are for those who want to push out a single branch after finishing work, even when the other branches are not yet ready to be pushed out. If you are working with other people to push into the same shared repository, you would want to use one of these.