# Git in a nutshell

## How version control works with git

The basic idea of how version control works in git is you have Git software on your system, located in a directory like usr/bin, and a git repository for each project you want to version control. A repository is essentially a fancy word for a database that keeps track of all your project's changes. The Git repository is stored in a .git directory in the root of the project. The .git directory contains all the information needed to version control your project.&#x20;



<figure><img src="../.gitbook/assets/Group 139.png" alt=""><figcaption></figcaption></figure>

## Obtaining a git repository

* initialize
* copy

## Components of a Git project

* working tree
* Staging area (technical term is index)
* Commits (i.e., snapshots of project)

<figure><img src="../.gitbook/assets/Group 141 (2).png" alt="" width="563"><figcaption></figcaption></figure>

## Commits, not autosave



### Committing is a two step process



## Remotes

* repos can exchange data between each other
* purpose is to enable collboaration



## Collaborative model



### Collaboration in git

A fundamental aspect of git is it's support for collaboration. For example, it might be two students collaborating on an assignment.

The basic idea of collaboration is for two repositories to be able to exchange data between each other.&#x20;

In git terminology, the repository you’re working in is called the local repository, while the repository you’re interacting with is called the remote repository. Git supports two basic operations: pushing and pulling. Pushing is when you upload data to a remote repository, while pulling is when you download. \


{% hint style="warning" %}
Note that a remote repository may be loicated on the same computer.
{% endhint %}

## Central workflow

It is theoretically possible for any two repositories to exchange data with each other directory. For example, two students on armlab. Each student can theoretically push and pull to the other one. In this context, the repository the student is working in is their local repo, and the other students is a remote repo. In practice this wouldn't work, since you don't have write access to their directory, but that's a filesystem barrier, not a git barrier. For arguments sake, let's assume each student has access permissions to the other students directories. It would still be a bad idea, since a remote repository should be bare. In other words, no one should work in the remote repository.  (See here for an example of why.) [http://htmlpreview.github.io/?https://github.com/sitaramc/sitaramc.github.com/blob/dce410b2a2804723676db9cabd7bb506b6d9ba05/concepts/bare.html](http://htmlpreview.github.io/?https://github.com/sitaramc/sitaramc.github.com/blob/dce410b2a2804723676db9cabd7bb506b6d9ba05/concepts/bare.html).&#x20;



Thus, the standard collboration workflow is to do so via a central, bare repository--that is, one thatr neither you nor anyone else works in.&#x20;

\


Central repositories are typically hosted on sites like GitHub, which is easily accessible to anyone in the world. However, there’s no reason it has to be GitHub. It can be any server that all collaborators have appropriate access to.&#x20;





\


Putting it all together, we can add a fourth box to our previous diagram, representing a remote repository.

going to have to explain how evrything goes through local repo



Notice that the remote repository does not have a working tree or an index, since it's a bare repository.
