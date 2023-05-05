# Acquiring a Git Repository

There are two ways you can acquire a Git repository:&#x20;

1. You can create a new Git repository.&#x20;
2. You can copy an existing Git repository.

Creating a repository means initializing a Git repository for a project that is not currently under Git version control; in contrast, copying a Git repository means duplicating an existing repository.

We will start by creating a Git repository, and we will use that to illustrate the fundamentals of the Git workflow. We will then cover copying or cloning, an existing Git repository.&#x20;

## Creating a Git Repository

The process of creating a Git repository is extremely simple. You simply navigate to the directory whose contents you want to version control and invoke `git init`. For example, to create a Git repository in your home directory, you'd perform these steps:

```bash
cd ~
git init 
```

Your home directory will now contain a _.git_ subdirectory, which contains your Git repository. You can confirm this by invoking _ls -a_.

An important thing to recognize with Git is that Git does not automatically save any content from your working directory into the repository. In the above example, nothing from your home directory will automatically be saved into your git repository. To save the contents, you must manually tell Git to do so.&#x20;

Saving is a two-step process involving _Staging_ and _committing._ In the staging step, you selectively choose the files from the working directory whose contents you want to save and add them to an area called the _index_ or _staging area_. You can stage individual files or a group of files. Once you have staged the files, the next step is to _commit_ them. Committing is the process of permanently saving the staged changes to the repository. This creates a new snapshot in the repository history.&#x20;

The reason there is an intermede space for staging files is that it allows you to review, group, or organize the changes before they are permanently saved. Committing is the process of permanently saving the staged changes to the repository or project history. This typically involves adding a descriptive message to explain the changes made and creating a unique identifier (commit ID) for the set of changes.

## Exercise&#x20;

We will practice basic Git commands using a directory named _git\_practice_ containing 3 files in it: _hello.c_, _circle1.c_, and _circle2.c_.&#x20;

To obtain the git\_practice directory, simply paste the following code block on the command line.

```bash
git clone https://github.com/avigewirtz/git_practice.git && cd git_practice && rm -rf .git
```

Your working directory will now be _git\_practice_. First, invoke `ls -a`, and notice that there is no _.git_ subdirectory:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 3.56.14 PM.png" alt=""><figcaption></figcaption></figure>

To create a Git repository, simply invoke `git init`:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 3.57.17 PM.png" alt=""><figcaption></figcaption></figure>

You will not have a Git repository. Invoke ls -a again, Now invoke ls -a again, and notice that git\_practice now contains a .git subdirectory:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 3.59.00 PM.png" alt=""><figcaption></figcaption></figure>

Now invoke `git status`, a useful command that allows you to view the state of your working directory and the staging area:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 4.00.05 PM (1).png" alt=""><figcaption></figcaption></figure>

All files that have not previously been staged will be listed as untracked files. For now, we will focus on only one aspect of the `git status` output: Untracked files. Any file that has not previously been staged to Git is untracked. To get Git to begin tracking it, you must stage them.&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 7.35.05 PM.png" alt=""><figcaption></figcaption></figure>

You can now commit them with the `git commit` command. When you commit, you also have to provide a commit message, which serves to document the changes you made. You can do so by supplying the -m option followed by quotation marks, inside which the message goes:



<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 7.38.50 PM.png" alt=""><figcaption></figcaption></figure>

Now when you invoke git status, you'll get a message letting you know that your working tree is clean:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 7.39.56 PM.png" alt=""><figcaption></figcaption></figure>

Case 1: Adding a new file

Say you add a new file, file1.txt, to the working directory. In the following example, I add the file with the touch command. If you invoke git status, you'll notice that file1.txt is Untracked:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 4.02.30 PM.png" alt=""><figcaption></figcaption></figure>

Case 2: modifying a file

Now say you modify the hello.c file by changing "Hello, world" to "Hello, everyone". Invokking Git status, you'll see that hello.c is now classified under "changes not staged for commit." To include the changes in the next commit, you must add it again.&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 4.03.19 PM.png" alt=""><figcaption></figcaption></figure>

A simple shortcut is if you want to add all new or modified files to the staging area is to use the \* wildcard instead of typing out each filename. Notice below that git status lists file1.txt and hello.c under "Changes to be commited". Any files in this section are in the staging area.&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 4.04.08 PM.png" alt=""><figcaption></figcaption></figure>

Now, say you modify hello.c again, by changing "Hello, everyone" back to "Hello, world". If you invoke git status, you will not see two versions of hello.c:&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 7.56.28 PM.png" alt=""><figcaption></figcaption></figure>

One of them is listed under "changed to be commits while the other is listed under "changes not staged for commit". The one staged for commit is the "Hello, everyone" version. The "Hello, world version is not staged for commit, since, if you modify a file after staging it, the modified version will not be reflected in the staged version. Rather, if you want the updated version to be included in the next commit, you must stage it again:&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 8.05.28 PM.png" alt=""><figcaption></figcaption></figure>

And notice that now the updated version that was previously not staged for commit is staged.&#x20;

You can now commit, which will save the updated&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 8.06.58 PM.png" alt=""><figcaption></figcaption></figure>

Now say you delete the file1.txt file using the rm command. Although it will be deleted from your working directory, it will not be deleted from your repository. If you invoke git status, you'll notice that file1.txt is listed under "Changes nor staged for commit":

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 8.20.08 PM.png" alt=""><figcaption></figcaption></figure>

Essentially, Git tracks that file1.txt has been deleted, but in order for you to have the deletion reflected in the repository, you need to stage it and then commit it:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 8.22.15 PM.png" alt=""><figcaption></figcaption></figure>

## Summary

* **Staging files**: There are two types of files you need to be staged with the `git add` command: untracked files, and modified files. Untracked files are files that are "new" to Git--that is, they haven't previously been staged. Modified files are files that were updated after they were last staged.&#x20;
* **Committing files**: The `git commit` command takes the files in the staging area and stores them permanently in your Git repository. Each commit represents a snapshot of your project's state.
* **Status of repository**: The `git status` command lists three categories of files.
  1. **Untracked files**: Files in the working directory that were not previously staged (i.e., "new" files).&#x20;
  2. **Changes not staged for commit**: Files that were modified or deleted since they were last staged.&#x20;
  3. **Changes to be committed**: Staged files that are ready to be committed.



## Local Git Workflow

The local Git workflow can be summarized as follows:

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

