# Git in a nutshell

## How version control works with git

The basic idea of how version control works in git is you have Git software on your system, located in a directory like usr/bin. If you want want to version control a project, you ask git to initialize a repository in the root directory of the project. The Git repository is stored in a .git directory in the root of the project. A repository is essentially a fancy word for a local database that keeps snapshots of your project's content--files and directories--at various points in time. Each snapshot is called a "commit." Figure 5.1 shows a filesystem with two projects under git version control: A1 and greetings. Each of them contain a .git directory in the project's root directory.&#x20;



<figure><img src="../.gitbook/assets/Group 139.png" alt=""><figcaption></figcaption></figure>

## You can duplicate an existing repository

Under the hood, git initializes an empty repository and populates it with the contents of the repository you're cloning.  To work on a project, you “clone” it from an existing repository, possibly over a network via protocols such as HTTP and SSH. Your clone is a full copy of the original, including all project history, completely functional on its own.

## Commits, not autosave

It's important to understand that Git does not monitor your work and constantly or periodically save a snapshot automatically. All saving must be done manually. This is called committing.&#x20;

### Committing is a two step process

Might think in order to save a snapshot you invoke "git commit" and it saves a snapshot of your current working tree. But that's not how it works. Applying changes to a repository is a two-step process: you add the changes to a staging area called the “index,” then commit those changes to the repository. The extra step allows you to easily apply just some of the changes in your current working files (including a subset of changes to a single file), rather than being forced to apply them all at once, or undoing some of those changes yourself before committing and then redoing them by hand. This encourages splitting changes up into better organized, more coherent and reusable sets.

## Components of a Git project

Summing things up, a Git project consists of three main components:&#x20;

* The working tree.&#x20;
* Staging area. The list of files to be included in your next commit.&#x20;
* Commits. Historical snapshots of your project since its inception.&#x20;

<figure><img src="../.gitbook/assets/Group 141 (3).png" alt="" width="563"><figcaption></figcaption></figure>

### Commit graph

The set of all commits in a repository forms a "commit graph." Can be simple, like the linear commit graph shown in Figure 1-2.



Figure 1-2. A linear commit graph

Or a complex graph involving many branches and merges, as shown in Figure 1-3.



The letters and numbers here represent commits, and arrows point from a commit to its parents. Commit A has no parents and is called a “root commit”; it was the initial commit in this repository’s history. Most commits have a single parent, indicat‐ ing that they evolved in a straightforward way from a single pre‐ vious state of the project, usually incorporating a set of related changes made by one person. Some commits, here just the one labeled E, have multiple parents and are called “merge commits.” This indicates that the commit reconciles the changes made on distinct branches of the commit graph, often combining contri‐ butions made separately by different people.



## Branches

## Remotes

Possible to push or pull data from other repo. In such a context, other repo is called remote.&#x20;

* repos can exchange data between each other
* purpose is to enable collaboration

With Git, sharing work between repositories happens via operations called “push” and “pull”: you pull changes from a remote repository and push changes to it. To work on a project, you “clone” it from an existing repository, possibly over a network via protocols such as HTTP and SSH. Your clone is a full copy of the original, including all project history, completely functional on its own. In particular, you do not need to contact the first repos‐ itory again in order to examine the history of your clone or com‐ mit to it—however, your new repository does retain a reference to the original one, called a “remote.” This reference includes the state of the branches in the remote as of the last time you pulled from it; these are called “remote tracking” branches. If the orig‐ inal repository contains two branches named master and topic, their remote-tracking branches in your clone appear qualified with the name of the remote (by default called “origin”): origin/ master and origin/topic.

Most often, the master branch will be automatically checked out for you when you first clone the repository; Git initially checks out whatever the current branch is in the remote repository. If you later ask to check out the topic branch, Git sees that there isn’t yet a local branch with that name—but since there is a remote- tracking branch named origin/topic, it automatically creates a branch named topic and sets origin/topic as its “upstream” branch. This relationship causes the push/pull mechanism to keep the changes made to these branches in sync as they evolve in both your repository and in the remote.

Overview | 5

When you pull, Git updates the remote-tracking branches with the current state of the origin repository; conversely, when you push, it updates the remote with any changes you’ve made to corresponding local branches. If these changes conflict, Git prompts you to merge the changes before accepting or sending them, so that neither side loses any history in the process.

If you’re familiar with CVS or Subversion, a useful conceptual shift is to consider that a “commit” in those systems is analogous to a Git “push.” You still commit in Git, of course, but that affects only your repository and is not visible to anyone else until you push those commits—and you are free to edit, reorganize, or de‐ lete your commits until you do so.

## Collaborative workflows

Being a distributed system, allows for many workflows.

### Collaboration in git

A fundamental aspect of git is it's support for collaboration. For example, it might be two students collaborating on an assignment.

The basic idea of collaboration is for two repositories to be able to exchange data between each other.&#x20;

In git terminology, the repository you’re working in is called the local repository, while the repository you’re interacting with is called the remote repository. Git supports two basic operations: pushing and pulling. Pushing is when you upload data to a remote repository, while pulling is when you download. \


{% hint style="warning" %}
Note that a remote repository may be loicated on the same computer.
{% endhint %}

## Centralized workflow

It is theoretically possible for any two repositories to exchange data with each other directory. For example, two students on armlab. Each student can theoretically push and pull to the other one. In this context, the repository the student is working in is their local repo, and the other students is a remote repo. In practice this wouldn't work, since you don't have write access to their directory, but that's a filesystem barrier, not a git barrier. For arguments sake, let's assume each student has access permissions to the other students directories. It would still be a bad idea, since a remote repository should be bare. In other words, no one should work in the remote repository.  (See here for an example of why.) [http://htmlpreview.github.io/?https://github.com/sitaramc/sitaramc.github.com/blob/dce410b2a2804723676db9cabd7bb506b6d9ba05/concepts/bare.html](http://htmlpreview.github.io/?https://github.com/sitaramc/sitaramc.github.com/blob/dce410b2a2804723676db9cabd7bb506b6d9ba05/concepts/bare.html).&#x20;



Thus, the standard collboration workflow is to do so via a central, bare repository--that is, one thatr neither you nor anyone else works in.&#x20;

\


Central repositories are typically hosted on sites like GitHub, which is easily accessible to anyone in the world. However, there’s no reason it has to be GitHub. It can be any server that all collaborators have appropriate access to.&#x20;





\


Putting it all together, we can add a fourth box to our previous diagram, representing a remote repository.

going to have to explain how evrything goes through local repo



Notice that the remote repository does not have a working tree or an index, since it's a bare repository.
