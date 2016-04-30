---
layout: page
title: Version Control with Git
subtitle: Branching and Merging
minutes: 5
---
> ## Learning Objectives {.objectives}
>
> *   Create and switch to new branches
> *   Merge changes from one branch to another

***This part is still under heavy construction, sorry.***

Branching in Git is one of its many great features. If you have used other version control systems, it's probably helpful to forget most of what you think about branches - in fact, it may be more helpful to think of them practically as *contexts* since that is how you will most often be using them. When you checkout different branches, you change contexts that you are working in and you can quickly context-switch back and forth between several different branches.

In a nutshell you can create a branch with `git branch (branchname)`, switch into that context with `git checkout (branchname)`, record commit snapshots while in that context, then can switch back and forth easily.

When you switch branches, Git replaces your working directory with the snapshot of the latest commit on that branch so you don't have to have multiple directories for multiple branches. You merge branches together with `git merge`. You can easily merge multiple times from the same branch over time, or alternately you can choose to delete a branch immediately after merging it.

* **git branch** - list, create, and manage working contexts
* **git checkout** - switch to a new branch context
* **git merge** - combine commits from two branches

---

#### Branches

The `git branch` command is a general branch management tool for Git and can do several different things. We'll cover the basic ones that you'll use most - listing branches, creating branches and deleting branches. We will also cover basic `git checkout` here which switches you between your branches.

Without arguments, `git branch` will list out the local branches that you have. The branch that you are currently working on will have a star next to it and if you have coloring turned on, will show the current branch in green.

~~~ {.bash}
$ git branch
~~~
~~~ {.output}
* master
~~~

This means that we have a 'master' branch and we are currently on it. When you run `git init` it will automatically create a 'master' branch for you by default, however there is nothing special about the name - you don't actually have to have a 'master' branch but since it's the default that is created, most projects do.

Now let's create a new branch.

~~~ {.bash}
$ git checkout -b bugfixes
~~~
~~~ {.output}
Switched to a new branch 'bugfixes'
~~~

Whoa! The command to create and immediately switch to a new branch is `git checkout -b ...` and not `git branch`.  It turns out, you can use `git branch branchname` to create a branch, but that won't switch you to the new branch context. It's easier to just use `git checkout -b` instead.  This is one of those weird Git things you just get used to.

Again, switching to a new branch changes your *context*. You are still in the same working directory; it's not like you've moved to a different folder. The *contents of your folder*, though, will reflect whatever is in the HEAD of the branch you just switched to. This means that the files and folders in your working directory will actually change to match the branch context.

This gets more clear when you start adding and removing files in a branch, and then switch back to master:


~~~ {.bash}
$ git checkout -b newfiles
Switched to a new branch 'newfiles'
$ echo "new stuff" > extra-file.txt
$ echo "more new stuff" > extra-file-2.txt
$ ls
README   hello.rb extra-file.txt extra-file-2.txt
$ git commit -am 'add the new files'
[newfiles 62c27cd] add the new files
 2 files changed, 2 insertions(+)
 create mode 100644 extra-file-2.txt
 create mode 100644 extra-file.txt
$ git checkout master
Switched to branch 'master'
$ ls
README   hello.rb
~~~

Switching to the master branch makes those two new files seemingly "disappear". Those files are only present in the newfiles branch -- they aren't in any commits in the master branch.

#### Merging branches

Once you have work isolated in a branch, you will eventually want to incorporate it into your main branch. You can merge any branch into your current branch with the `git merge` command. Let's take as a simple example the 'newfiles' branch from above. If we create a branch and add files in it and commit our changes to that branch, those changes are isolated from our main ('master') branch. To include those changes in your 'master' branch, you can just merge in the 'newfiles' branch.

~~~ {.bash}
$ git branch
* master
  newfiles
$ ls
README   hello.rb
$ git merge newfiles
Updating 8bd6d8b..8f7c949
Fast-forward
 extra-file.txt   |    1 -
 extra-file-2.txt |    1 -
 2 files changed, 2 insertions(+), 0 deletions(-)
 create mode 100644 extra-file.txt
 create mode 100644 extra-file-2.txt
$ ls
README   hello.rb extra-file.txt extra-file-2.txt
~~~

Now the commits from the newfiles branch have been incorporated into our current, master, branch and context. We can see both added files now.

Of course, this doesn't just work for simple file additions and deletions. Git will merge file modifications as well - in fact, it's very good at it. I'll leave the more complex merge stuff for the next advanced course. =)

#### Deleting branches

Removing a branch is as easy as `git branch -d branchname`.
