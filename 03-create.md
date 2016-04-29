---
layout: page
title: Version Control with Git
subtitle: Creating a Repository
minutes: 10
---
> ## Learning Objectives {.objectives}
>
> *   Create a local Git repository.

Once Git is configured, we can start using it.

There are two main ways to get a Git repository. One way is to simply initialize a new one from an existing directory, such as a new project or an existing project that's new to source control. The second way is to "clone" one from a public Git repository, as you would do if you wanted a copy or wanted to work with someone on a project. We will cover the first of those here, and we'll get to collaboration in a later section.

#### Initializing a new repository

If you are starting from scratch with an empty directory, or if you have an existing folder of files that isn't currently managed with Git, the first step is to tell Git that it's time to turn that folder into a **git repository** — which means that for everything in that folder, Git can track changes, create snapshots, and keep a history of who changes what and when, from this point forward.

Let's create a new directory for our tutorial on our desktop, and then move into that directory.

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

