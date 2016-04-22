---
layout: page
title: Version Control with Git
subtitle: Automated Version Control
minutes: 5
---
> ## Learning Objectives {.objectives}
>
> *   Understand the benefits of an automated version control system.
> *   Understand the basics of how Git works.

We'll start by exploring how version control can be used
to keep track of what one person did and when.
Even if you aren't collaborating with other people,
automated version control is much better than this situation:

[![Piled Higher and Deeper by Jorge Cham, http://www.phdcomics.com](fig/phd101212s.gif)](http://www.phdcomics.com)

"Piled Higher and Deeper" by Jorge Cham, http://www.phdcomics.com

We've all been in this situation before: it seems ridiculous to have multiple nearly-identical versions of the same document. Some word processors let us deal with this a little better, such as Microsoft Word's "Track Changes" or Google Docs' version history.

### Starting from scratch

Let's start from scratch. Assume you are designing a new source code management system. How did you do basic version control before you used a tool for it? Chances are that you simply copied your project directory to save what it looked like at that point.

~~~ {.bash}
 $ cp -R project project.bak
~~~

That way, you can easily revert files that get messed up later, or see what you have changed by comparing what the project looks like now to what it looked like when you copied it.

If you are really paranoid, you may do this often, maybe putting the date in the name of the backup:

~~~ {.bash}
 $ cp -R project project.2010-06-01.bak
~~~

In that case, you may have a bunch of snapshots of your project that you can compare and inspect from. You can even use this model to fairly effectively share changes with someone. If you zip up your project at a known state and put it on your website, other developers can download that, change it and send you a patch pretty easily.

~~~ {.bash}
 $ wget http://example.com/project.2010-06-01.zip
 $ unzip project.2010-06-01.zip
 $ cp -R project.2010-06-01 project-my-copy
 $ cd project-my-copy
 $ (change something)
 $ diff project-my-copy project.2010-06-01 > change.patch
 $ (email change.patch)
~~~

Now the original developer can apply that patch to their copy of the project and they have your changes. This is how many open source projects have been collaborated on for several years.

This actually works fairly well, so let's say we want to write a tool to make this basic process faster and easier. Instead of writing a tool that versions each file individually, we would probably write one that makes it easier to store snapshots or "save points" of our entire project, without having to copy the whole directory each time.

This is essentially what Git is. You tell Git you want to save a snapshot of your project with the git commit command and it basically records a manifest of what all of the files in your project look like at that point. Then most of the commands work with those manifests to see how they differ or pull content out of them, etc.

### Saving snapshots of your work

Git works on entire projects, but it's easiest to start thinking about it one file at a time. Git starts with a base version of a document and then saves just the changes you made at each step of the way. You can think of it as a tape: if you rewind the tape and start at the base document, then you can play back each change and end up with your latest version.

![Changes are saved sequentially](fig/play-changes.svg)

Once you think of changes as separate from the document itself, you can then think about "playing back" different sets of changes onto the base document and getting different versions of the document. For example, two users can make independent sets of changes based on the same document.

![Different versions can be saved](fig/versions.svg)

If there aren't conflicts, you can even try to play two sets of changes onto the same base document.

![Multiple versions can be merged](fig/merge.svg)

A version control system is a tool that keeps track of these changes for us and
helps us version and merge our files. It allows you to
decide which changes make up the next version, called a
[commit](reference.html#commit), and keeps useful metadata about them. The
complete history of commits for a particular project and their metadata make up
a [repository](reference.html#repository). Repositories can be kept in sync
across different computers facilitating collaboration among different people.

This example just showed changes happening in one file for simplicity, but Git can track the changes in your entire project: it's more like a save point in a videogame. Each game save point can store your progress, your items, your stats, and your location -- all together.


> ## The long history of version control systems {.callout}
>
> Automated version control systems are nothing new.
> Tools like RCS, CVS, or Subversion have been around since the early 1980s and are used by many large companies.
> However, many of these are now becoming considered as legacy systems due to various limitations in their capabilities.
> In particular, the more modern systems, such as Git and [Mercurial](http://swcarpentry.github.io/hg-novice/)
> are *distributed*, meaning that they do not need a centralized server to host the repository.
> These modern systems also include powerful merging tools that make it possible for multiple authors to work within
> the same files concurrently.
