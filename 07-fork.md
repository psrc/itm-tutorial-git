---
layout: page
title: Version Control with Git
subtitle: 3. GitHub Workflow - Forks and Pull Requests
minutes: 25
---
> ## Learning Objectives {.objectives}
> *  Understand the GitHub-specific concept of a personal fork
> *  Understand the GitHub-specific concept of a Pull Request
> *  Collaborate using GitHub fork/pull workflow

Git allows massive distribution of code. This is often a new idea for people used to tight ownership of closed-source software code, but in 2016 it is more and more prevalent in scientific research to do things in an open manner.

There will be many cases where you are not going to get write access to a repository on GitHub:

* The repo is owned by an agency or team that you're not a part of
* The repo is for a big public project with many many contributors who may or may not even know each other
* You're just "lurking" — exploring someone else's project or code for your own reasons

#### Forking Code

GitHub has come up with an ingenious add-on to the Git workflow model, known as personal forks.  A "fork" is just a copy of someone else's repository on GitHub, that belongs to you. At the moment you fork a repository, your fork is an exact replica of the other project, with one important difference: you have write-access to it. The original owner doesn't need to give you permission to do so, and you can modify that code any way you see fit because your changes stay local to your fork.

If you can see someone's repository on GitHub, you can fork it.

Let's fork some code!

1. Go to <https://github.com/billyc/git-lesson>
2. Find the FORK button in the upper right, to create your own fork of this project
3. Copy the clone URL from the bar (use the HTTPS version)

**The Difference between FORK and CLONE**

You've now got your own writable repository of someone else's code: in this case, a small repo that I created for this class. Only I have write access to the original repo on GitHub, but you now have your own fork on GitHub which you can play with.

To actually do anything with your fork, though, you still need to make a local clone of the code on your laptop.

~~~ {.bash}
$ cd
$ cd Desktop
$ git clone https://github.com/YOURNAME/git-lesson.git
~~~

Again, `git clone` creates a fresh local copy of a remote repository, which in this case is itself a fork of someone else's repository.

You'll see that this repo is just one simple Python script, and a folder `contributors` with text files from each contributor. Now, add a new text file to the contributors folder with your name in it.

~~~ {.bash}
$ cd git-lesson/contributors
$ nano myname.txt
$ (add your full name to the first line of that file)
~~~

and save, add, commit, and push your changes!
~~~ {.bash}
$ git add me.txt
$ git commit -m "added myself as a contributor to this project"
$ git push
~~~

You've added a new snapshot with the text file to your private fork, and pushed that change back up to GitHub.

#### Pull Request

The final step in GitHub workflow is to let the original owner know that you've made some important changes that you think deserve to be merged into the main repository. You do this with what's called a "pull request"

* Go back to GitHub and you'll see your project now has a new commit.
* Click the "New Pull Request" button and follow the on-screen instructions to send the original repo owner a message along with your request that they "pull" your latest changes.


> ## Difference between init and clone {.challenge}
>
> What's the difference?

> ## Difference between Fork and Clone {.challenge}
>
> What's the difference?

