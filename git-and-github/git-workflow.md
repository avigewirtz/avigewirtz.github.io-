# Git Workflow

We will demonstrate the Git workflow with a real example using a directory named git\_practice, containing 3 files in it: _hello.c_, _circle1.c_, and _circle2.c_. To obtain _git\_practice_, log into armlab and paste the following code block on the command line:

```bash
git clone https://github.com/avigewirtz/git_practice.git && cd git_practice
```

This will create a directory named git\_practice, which will be set as your working directory. First, invoke `ls -a.` You should get the following output:&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-05-03 at 3.59.00 PM.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (11).png" alt="" width="563"><figcaption></figcaption></figure>

## Working Tree



Each (non-bare) Git repository has an associated _working tree_. The working tree is simply the area where you work on the project. When you clone a Git repository or create a new one, a working tree is created in your local file system. In the previous example, the working tree is Survey (along with all its subdirectories).&#x20;

## Commits

Commits are the building blocks of a Git repository. Each commit represents a snapshot of the project at a certain point in time.&#x20;

```css
[A1, B1, C1]---[A2, B1, C1, D1]---[A2, B2, C1, D1]---[A3, B2, C2]---[A3, B3, C2, E1] 
```

It includes the snapshot of the files from the previous commit and the modifications you have staged (using `git add`) for the new commit.

There are two important things to recognize with commits Git:

1. A commit represents the latest commit + merged changes.&#x20;
2. All commits are manual.&#x20;



You tell Git which files to commit by first&#x20;



Saving content to the repository is a two-step process, involving _staging_ and _committing_.&#x20;

### Staging files

Staging is the process of selectively choosing the files you want Git to save a snapshot of and adding them to the _index_ or _staging area_. In this step, you specify each file you'd like to stage. Staging is accomplished with the `git add` command.&#x20;

```bash
git add FILE(S)
```

If you want to stage all (non-[ignored](important-git-commands/ignoring-files.md)) project files, you can save time by using the `*` [wildcard](../bash/useful-command-line-features.md#wildcards):

```bash
git add * # stages all non-ignored files and directories in the working directory
```

### Committing Files

_Committing_ is the process of permanently saving the snapshot of staged files to the repository. When you commit, Git records the timestamp of the commit, along with other information such as the commit author's name, email address, and a commit message.&#x20;

When you commit, you don't specify specific files to commit. Git commits all files in the staging area. Committing is accomplished with the `git commit` command:&#x20;

```bash
git commit
```

After pressing ENTER, Git will open your preferred text editor and prompt you for a _commit message_. A commit message is simply a user-defined message that serves to document the changes made to the repository. As such, commit messages should be descriptive.  &#x20;

A simpler way to commit is to specify the commit message along with the git commit command, as so:

```bash
git commit -m "COMMIT MESSAGE" 
```

Each commit has associated metadata such as a unique commit ID, the author's name and email address, the commit message, and the date and time of the commit. Commits represent the building blocks of a Git repository.

## Purpose of the Staging Area

The reason there is an intermede space for staging files is that it allows you to review, group, or organize the changes before they are permanently saved.&#x20;

## Exercise&#x20;

In this exercise, you will be introduced to the most fundamental Git commands. We will practice basic Git commands using a directory named _git\_practice_ containing 3 files in it: _hello.c_, _circle1.c_, and _circle2.c_.&#x20;

To obtain _git\_practice_, log into your development computer and paste the following code block on the command line:

```bash
git clone https://github.com/avigewirtz/git_practice.git && cd git_practice && rm -rf .git
```

This will copy _git\_practice_ to your working directory and then change your working directory to _git\_practice_. If you invoke `ls -a`, you will see three files: _circle1.c_, _circle2.c_, and _hello.c_; however, you will not see a _.git_ directory, since _git\_practice_ is not yet under Git version control.&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-05-03 at 3.56.14 PM.png" alt=""><figcaption></figcaption></figure>

To create a Git repository in _git\_practice_, invoke `git init`:

<figure><img src="../.gitbook/assets/Screenshot 2023-05-03 at 3.57.17 PM.png" alt=""><figcaption></figcaption></figure>

git\_practice will now have a Git repository. You can verify this by invoking ls -a again and confirming that there is a _.git_ subdirectory:&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-05-03 at 3.59.00 PM.png" alt=""><figcaption></figcaption></figure>

We will now introduce one of the most useful git commands: `git status`. Git status allows you to view the state of your working directory and the staging area.&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-05-03 at 4.00.05 PM (1).png" alt=""><figcaption></figcaption></figure>

All files that have not previously been staged will be listed as untracked files. For now, we will focus on only one aspect of the `git status` output: Untracked files. Any file that has not previously been staged to Git is untracked. To get Git to begin tracking it, you must stage them.&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-05-03 at 7.35.05 PM.png" alt=""><figcaption></figcaption></figure>

You can now commit them with the `git commit` command. When you commit, you also have to provide a commit message, which serves to document the changes you made. You can do so by supplying the -m option followed by quotation marks, inside which the message goes:



<figure><img src="../.gitbook/assets/Screenshot 2023-05-03 at 7.38.50 PM.png" alt=""><figcaption></figcaption></figure>

Now when you invoke git status, you'll get a message letting you know that your working tree is clean:

<figure><img src="../.gitbook/assets/Screenshot 2023-05-03 at 7.39.56 PM.png" alt=""><figcaption></figcaption></figure>

Case 1: Adding a new file

Say you add a new file, file1.txt, to the working directory. In the following example, I add the file with the touch command. If you invoke git status, you'll notice that file1.txt is Untracked:

<figure><img src="../.gitbook/assets/Screenshot 2023-05-03 at 4.02.30 PM.png" alt=""><figcaption></figcaption></figure>

Case 2: modifying a file

Now say you modify the hello.c file by changing "Hello, world" to "Hello, everyone". Invokking Git status, you'll see that hello.c is now classified under "changes not staged for commit." To include the changes in the next commit, you must add it again.&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-05-03 at 4.03.19 PM.png" alt=""><figcaption></figcaption></figure>

A simple shortcut is if you want to add all new or modified files to the staging area is to use the \* wildcard instead of typing out each filename. Notice below that git status lists file1.txt and hello.c under "Changes to be commited". Any files in this section are in the staging area.&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-05-03 at 4.04.08 PM.png" alt=""><figcaption></figcaption></figure>

Now, say you modify hello.c again, by changing "Hello, everyone" back to "Hello, world". If you invoke git status, you will not see two versions of hello.c:&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-05-03 at 7.56.28 PM.png" alt=""><figcaption></figcaption></figure>

One of them is listed under "changed to be commits while the other is listed under "changes not staged for commit". The one staged for commit is the "Hello, everyone" version. The "Hello, world version is not staged for commit, since, if you modify a file after staging it, the modified version will not be reflected in the staged version. Rather, if you want the updated version to be included in the next commit, you must stage it again:&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-05-03 at 8.05.28 PM.png" alt=""><figcaption></figcaption></figure>

And notice that now the updated version that was previously not staged for commit is staged.&#x20;

You can now commit, which will save the updated&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-05-03 at 8.06.58 PM.png" alt=""><figcaption></figcaption></figure>

Now say you delete the file1.txt file using the rm command. Although it will be deleted from your working directory, it will not be deleted from your repository. If you invoke git status, you'll notice that file1.txt is listed under "Changes nor staged for commit":

<figure><img src="../.gitbook/assets/Screenshot 2023-05-03 at 8.20.08 PM.png" alt=""><figcaption></figcaption></figure>

Essentially, Git tracks that file1.txt has been deleted, but in order for you to have the deletion reflected in the repository, you need to stage it and then commit it:

<figure><img src="../.gitbook/assets/Screenshot 2023-05-03 at 8.22.15 PM.png" alt=""><figcaption></figcaption></figure>

## Summary

* **Staging files**: There are two types of files you need to be staged with the `git add` command: untracked files, and modified files. Untracked files are files that are "new" to Git--that is, they haven't previously been staged. Modified files are files that were updated after they were last staged.&#x20;
* **Committing files**: The `git commit` command takes the files in the staging area and stores them permanently in your Git repository. Each commit represents a snapshot of your project's state.
* **Status of project files**: The `git status` command lists three categories of files in the working tree:
  1. **Untracked files**: Files in the working directory that were not previously staged (i.e., "new" files).&#x20;
  2. **Changes not staged for commit**: Files that were modified or deleted since they were last staged.&#x20;
  3. **Changes to be committed**: Staged files that are ready to be committed.



## Local Git Workflow

The local Git workflow can be summarized as follows:

<figure><img src="../.gitbook/assets/image (7) (1) (1).png" alt=""><figcaption></figcaption></figure>
