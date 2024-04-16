# Git in a nutshell

## How version control works with git



Workspace with an associated repository

The basic idea of how version control is done in git is that the project under version control has a .git directory in the root of the project's workspace. Inside the .git directory is a repository, which is essentially a fancy word for a database that keeps track of all your project's changes.&#x20;

### Obtaining a git repository

prob better to mention both nethods here but not go over commands. or idk because later i go over commands

### Initializing a Git repository

To initialize a Git repository for a project, you simply invoke `git init` within the project directory. For example, suppose we're in the directory `MyProject` with the files foo and bar. If we invoke:

```
git init
```

a repository will be created for our project. You can verify by invoking `ls -a`, and you should see a `.git` directory among the listings:

```
ls -a
. .. .git foo bar
```

## Repositories can be copied

Instead of initliazing a repository from sctrach, you can clone an existing repository. for example, in cos217, you copy repository's from cos217 GItHub account.&#x20;

The process of cloning a repository is extremely straightforward as well. You simply navigate to the directory you want the clone to reside in and invoke `git clone` with the source repository's URL as an argument. A GitHub URL has the following format:

```
https://github.com/GITHUB_USERNAME/REPOSITORY_NAME.git
```

GITHUB\_USERNAME represents the username of the GitHub account you are cloning from, and REPOSITORY\_NAME represents the name of the source repository. For example, if you're cloning the Survey repository from the COS217 GitHub account, you'd replace GITHUB\_USERNAME with cos217 and REPOSITORY\_NAME with _survey_:

```bash
git clone https://github.com/cos217/survey.git 
```

Upon success, you will get the following output:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-04 at 8.00.49 PM (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Note that the arguments for the GitHub account and repository names are case-insensitive--that is, COS217, cos217, and Cos217 all refer to the same GitHub account (and the same applies to variations of _survey_).

## Commits, not autosave



you probably have some expirience with tools like google docs, that autosaves your work and periodically saves a version you can revert to. Git does neither of these. All version control work is manual.&#x20;

Going back to our previous example, neither foo nor bar will be automaticvally saved by git. The git repository we created is "empty." To save a snapshot of your project at any point in time, you have to do a commit.&#x20;

## Committing is a two step process

When you invoke git commit, it only saves the files that are listed in the index or staging area, so called because it contains a list of the files that are to be included in the next commit. Going back to our example again, if we wanted to commit foo and bar, we have to first add them to the staging area. This  is done by invoking git add followed by the names of the files we want to stage:

```
git add foo bar
```

If you know you want to add all files of your project, you can use the . shortcut:

```
git add .
```

. means&#x20;

The purpose of the staging area is to allow you to choose which files go in the next commit. Sometimes, you don't want to commit all files. For example, say we only wanted to include foo in the next commit. We'd do so by adding only foo to the staging area and then commiting.





summing it all up, a project under git version control contains three components:

* The **working tree** provides a view of one version of the project (the files that you work on and see).
* The **index** intermediates between the repository and the working tree, helping you prepare changes for your next commit.
* The repository itself



<figure><img src="../../.gitbook/assets/image (7) (1) (1).png" alt=""><figcaption></figcaption></figure>

### Collaboration in git

A fundamental aspect of git is it's support for collaboration. For example, it might be two students collaborating on an assignment.

The basic idea of collaboration is for two repositories to be able to exchange data between each other.&#x20;

In git terminology, the repository you’re working in is called the local repository, while the repository you’re interacting with is called the remote repository. Git supports two basic operations: pushing and pulling. Pushing is when you upload data to a remote repository, while pulling is when you download. \


{% hint style="warning" %}
Note that a remote repository may be loicated on the same computer.
{% endhint %}

## Central Repository&#x20;

It is theoretically possible for any two repositories to exchange data with each other directory. For example, two students on armlab. Each student can theoretically push and pull to the other one. In this context, the repository the student is working in is their local repo, and the other students is a remote repo. In practice this wouldn't work, since you don't have write access to their directory, but that's a filesystem barrier, not a git barrier. For arguments sake, let's assume each student has access permissions to the other students directories. It would still be a bad idea, since a remote repository should be bare. In other words, no one should work in the remote repository.  (See here for an example of why.) [http://htmlpreview.github.io/?https://github.com/sitaramc/sitaramc.github.com/blob/dce410b2a2804723676db9cabd7bb506b6d9ba05/concepts/bare.html](http://htmlpreview.github.io/?https://github.com/sitaramc/sitaramc.github.com/blob/dce410b2a2804723676db9cabd7bb506b6d9ba05/concepts/bare.html).&#x20;



Thus, the standard collboration workflow is to do so via a central, bare repository--that is, one thatr neither you nor anyone else works in.&#x20;

\


Central repositories are typically hosted on sites like GitHub, which is easily accessible to anyone in the world. However, there’s no reason it has to be GitHub. It can be any server that all collaborators have appropriate access to.&#x20;

\


Putting it all together, we can add a fourth box to our previous diagram, representing a remote repository.

<figure><img src="../../.gitbook/assets/Group 120.png" alt=""><figcaption></figcaption></figure>

going to have to explain how evrything goes through local repo



Notice that the remote repository does not have a working tree or an index, since it's a bare repository.
