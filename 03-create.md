---
layout: page
title: Version Control with Git
subtitle: Creating a Repository
minutes: 10
---
> ## Learning Objectives {.objectives}
>
> *   Understand the difference between Git and GitHub.
> *   Create a local Git repository.
> *   Clone (make a copy of) an existing Git repository.

It's increasingly likely that your first real exposure to Git will be because you want to download or maybe even modify some code that is available on the website [Github.com](http://github.com).

What is GitHub, and how is it different from Git itself? Well:

**Git** is a system for storing and managing snapshots of your files. It runs locally on your computer, and has both command-line and GUI tools that help you to use it. Once you've installed Git on your computer, you can use it to manage any files want. Everything can stay local on your computer, so you don't need to worry about whether your stuff is public, open-source, private, sensitive -- it doesn't matter. Git is just a way to help you manage your files. You can use Git to share files with others, too, but only if you want to use it that way.

**GitHub** is a popular website where you can upload a copy of your Git repositories. It is a Git repository "hosting service", which offers all of the revision control and source code management  functionality of Git, as well as adding its own features. You don't need to use Github to get the benefits of Git, but you do have to be comfortable with Git before anything on the Github website will make sense.

[GitHub](http://github.com) is run by the company Github Inc., and Github is free for open source files — and this means that *anything you upload to Github with a free account will be visible for everyone on the Internet to see and download*. Github does, of course, offer paid accounts too which allow private cloud storage for repositories that can't be out in the open.

There are many other websites which offer similar services, such as [bitbucket](http://bitbucket.org) and [gitlab](http://www.gitlab.com).

Let's start simple, by learning just the basics of Git itself first.

#### Cloning an existing repository

https://github.com/psrc/make-lesson

#### Initializing a new repository

Once Git is configured, we can start using it.

If you are starting from scratch with an empty directory, or if you have an existing folder of files that isn't currently managed with Git, the first step is to tell Git that it's time to turn that folder into a **repository** — which means that Git will track changes, create snapshots, and keep a history of who changes what and when for the files in that folder, from this point forward.

Let's create a new directory for our work on our desktop, and then move into that directory.

Open a terminal window and type:

~~~ {.bash}
$ cd
$ cd Desktop
$ mkdir planets
$ cd planets
~~~

Then we tell Git to make `planets` a [repository](reference.html#repository)&mdash;a place where
Git can store versions of our files:

~~~ {.bash}
$ git init
~~~

If we use `ls` to show the directory's contents,
it appears that nothing has changed:

~~~ {.bash}
$ ls
~~~

But if we add the `-a` flag to show everything,
we can see that Git has created a hidden directory within `planets` called `.git`:

~~~ {.bash}
$ ls -a
~~~
~~~ {.output}
.	..	.git
~~~

Git stores information about the project in this special sub-directory.
If we ever delete it,
we will lose the project's history.

We can check that everything is set up correctly
by asking Git to tell us the status of our project:

~~~ {.bash}
$ git status
~~~
~~~ {.output}
# On branch master
#
# Initial commit
#
nothing to commit (create/copy files and use "git add" to track)
~~~

> ## Places to Create Git Repositories {.challenge}
>
> Dracula starts a new project, `moons`, related to his `planets` project.
> Despite Wolfman's concerns, he enters the following sequence of commands to
> create one Git repository inside another:
>
> ~~~ {.bash}
> cd             # return to home directory
> mkdir planets  # make a new directory planets
> cd planets     # go into planets
> git init       # make the planets directory a Git repository
> mkdir moons    # make a sub-directory planets/moons
> cd moons       # go into planets/moons
> git init       # make the moons sub-directory a Git repository
> ~~~
>
> Why is it a bad idea to do this?
> How can Dracula "undo" his last `git init`?

