# Local Git Workflow

## Initializing a repository

Suppose we have a project named greetings, which consists of the files shown in Figure 3. Two files: hello.txt, which simply contains the word "hello", and hi.txt which contains the word "hi".&#x20;

<details>

<summary>Creating your own version of greetings</summary>

if you want to follow along, simple open a terminal window and invoke the following four commands:

```bash
mkdir greetings
cd greetings
echo "hello" > hello.txt
echo "hi" > hi.txt
```

This will create a directory named greetings and and populate it with hello.txt and hi.txt.&#x20;

</details>



We want to version control it with git. Initializing a repository is perhaps the simplest task in git. Simply invoke:

```
~/greetings> git init
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint: 
hint: 	git config --global init.defaultBranch <name>
hint: 
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint: 
hint: 	git branch -m <name>
Initialized empty Git repository in /Users/avigewirtz/greetings/.git/
~/greetings>
```

note that init is short for initialize. If we now invoke ls -a, we will see a directory named .git:





dirty

A [working tree](https://git-scm.com/docs/gitglossary#def\_working\_tree) is said to be "dirty" if it contains modifications which have not been [committed](https://git-scm.com/docs/gitglossary#def\_commit) to the current [branch](https://git-scm.com/docs/gitglossary#def\_branch).







## remote repository

A [repository](https://git-scm.com/docs/gitglossary#def\_repository) which is used to track the same project but resides somewhere else. To communicate with remotes, see [fetch](https://git-scm.com/docs/gitglossary#def\_fetch) or [push](https://git-scm.com/docs/gitglossary#def\_push).





This creates a new subdirectory named `.git` that contains all of your necessary repository files — a Git repository skeleton.&#x20;



<figure><img src="../../.gitbook/assets/Group 112.png" alt="" width="375"><figcaption></figcaption></figure>



All of our&#x20;

<figure><img src="../../.gitbook/assets/Group 114.png" alt="" width="563"><figcaption></figcaption></figure>















### Staging files

If you want to start version-controlling existing files (as opposed to an empty directory), you should probably begin tracking those files and do an initial commit. You can accomplish that with a few `git add` commands that specify the files you want to track, followed by a `git commit`:

```console
$ git add *.c
$ git add LICENSE
$ git commit -m 'Initial project version'
```

We’ll go over what these commands do in just a minute. At this point, you have a Git repository with tracked files and an initial commit.





`git add` is a command that allows you to stage changes in your working directory, preparing them to be committed to the repository. Staging changes means that you're telling Git you want to include those specific changes in the next commit. This is useful for organizing your work into logical units or separating unrelated changes.

In the following examples, we will use [Decomment](https://github.com/COS217/Decomment) repository as a reference:

1.  **Adding a file.** Suppose you've created a new file named `decomment.c` that contains the main implementation of the Decomment project. After creating the file, you would stage it using `git add`:

    ```bash
    git add decomment.c
    ```
2. **Modifying a file.**&#x20;
   * Suppose you've made changes to `decomment.c`, such as adding a new function or improving existing code. After making the changes, you would stage the modified file again:

```bash
git add decomment.c
```

* Similarly, suppose you've populated the readme file, as required at the end of the assignment. If you want to include the populated readme file in your Git repository, you would stage the updated file: git add read

```bash
git add readme
```

#### Common usage:

*   **Staging a single file:**

    ```bash
    git add FILE_NAME
    ```
*   **Staging multiple files:**

    ```bash
    git add FILE1 FILE2
    ```
*   **Staging all changes in the working directory:**

    ```bash
    git add .
    ```





In the first section of this tuturial, we will focus on a local git workflow. Start from the basics and explain evrything in depth. In this section, to keep evrything truly local, we will create a repository from scratch. It also helps you learn how git works.









As we mentioned earlier, a project under git version control can be divided into three components:

* The working tree
* The index
* The repository

The repository essentially consists of commits, or saved snapshots of your project. The staging area consists of a list of new or modified files that are to be included in your next commit. The working tree consists of all the files you're currently working with.&#x20;



Within the&#x20;

has three main comp

consists of three things--worktree, index, and repository.&#x20;



There are&#x20;



We'll explain the basics of git using entirely one repository.&#x20;

First, let's create a project directory, which we'll call git\_practice:

```
mkdir git_practice
cd git_practice
```





Assume local environment personal project you want to track.



Assume we have directory that looks like this.

You have a project you want to track.&#x20;



1. Create a repository.
2. Save a snapshot of your project to the repository.&#x20;
3. Edit your project.&#x20;
4. Save the new snapshot to your repository.&#x20;
5. Repeat steps 3-4 as necessary.&#x20;

Let's go over these steps one by one. We'll go over reverting to a previous snapshot later.&#x20;

## Creating a repository

Within the project directory, you create what is known as a repository by invoking `git init.` (init is short for initialize). This creates a subdirectory named .git, where the git repository is stored. A Git repository is essentially a database that holds all the necessary information for maintaining and managing a project's files and history.&#x20;

Since we just created the repository, it will be empty.&#x20;

## Saving files

An important thing to recognize that Git does not automatically save anything in our repository.  changes. In other words, it's not like an autosave, where every time you type your work is saved. We have to manually save our work. Our goal is to save the three files in our directory.

Saving work is a two step process, involving staging and committing. First, you have to tell git which files you want it to include in the saved snapshot of your directory. This is called staging. This may seem redundant, since you likely want to save all files. In this step, you selectively choose the changes you want to include in the next commit.

To stage, invoke git add followed by the names of the files you want to stage. In our case:

```
git add intmath.c testintmath.c
```

If you want to stage all relevant files, you can save time by using the `*` [wildcard](../../the-linux-command-line/useful-command-line-features.md#wildcards):

```bash
git add * 
```

To actually save the files, you invoke the git commit command. All files in the stagin area will be included in the commit. Git requires you to add a commit message with each commit. For first commit not much to say, but for later commits important.&#x20;

```bash
git commit -m "first commit" 
```

note that the quotation marks are part of the command.&#x20;



**Editing and Saving More Snapshots**

Now, let's assume we make a couple of changes to our project. For example, we modify testintmath.c, and we create a new file named circle.c. To save a new snapshot that reflects these changes, we invoke:

```
git add intmath.c circle.c
git commit -m "fixed bug in testintmath.c. added circle.c"
```

Notice that this time with git add, we need only list intmath.c. and circle.c. Any other file that was previously commited but hasn't changed is automatically a part of the new snapshot.&#x20;

















\










## Worktree

Every (non-bare) Git repository has an associated _worktree_ (also called _working tree_). The worktree is essentially synonymous with the working directory. It is the area you do all of your project development in.

The worktree is distinct from the repository. The repository serves as the area where the project's history is stored. You don't develop in the repository. Instead, you develop in the worktree, and whenever you are ready to save a snapshot of your project, you tell Git to copy the changes from the worktree into the repository. This is called _committing_.

## Commits

Commits are the foundation of a Git repository. Each commit represents a snapshot of the project at a certain point in time. This idea is illustrated in the Figure below, where each commit is represented as a version of the project.

<figure><img src="../../.gitbook/assets/snapshots-2.png" alt=""><figcaption><p>Courtesy of Git-SCM</p></figcaption></figure>

Each commit has a unique identifier, which is used by Git to reference it. Git records important information along with each commit, such as the timestamp of the commit, the author's name and email address, as well as the commit message, which is a short message provided by the commit author that serves to document the commit.

There are two important things to recognize with how commits work in Git:

1. **All commits must be done manually**. That is, Git does not automatically commit anything from the worktree. Consequently, whenever you create a new Git repository, the repository will initially be empty--that is, the files previously present in the directory, which are now in the worktree, will not automatically be committed to the Git repository. In fact, they will not even be _tracked_ or monitored by Git. Similarly, previously committed files are subsequently modified, the modified versions will not automatically be committed.
2. **Committing is a two-step process**. Before changes can be committed from the worktree to the repository, they must be added to an intermediate area called the _index_ or _staging area_. In this step, you selectively choose the changes you want to include in the next commit. This allows you to review, group, or organize the changes before you save them to the repository. When you commit changes, only changes that were staged are committed.

### Staging files

There are two types of files that have to be staged: untracked files and modified files. Untracked files are new files--that is, files that were not previously in the repository. Modified files, on the other hand, are those that were previously in the repository but whose contents have since been modified.

Staging is accomplished with the `git add` command, where you specify each of the untracked or modified files you want to stage:

```bash
git add FILE(S)
```

If you want to stage all relevant files, you can save time by using the `*` [wildcard](../../the-linux-command-line/useful-command-line-features.md#wildcards):

```bash
git add * 
```









### Committing Files

When you commit, you don't selectively choose which files to commit. You simply commit all files in the staging area. Committing is accomplished with the `git commit` command:

```bash
git commit
```

After pressing ENTER, Git will open your preferred text editor and prompt you for a commit message, which is simply a user-defined message whose purpose is to document the changes made to the repository. As such, commit messages should be descriptive.

A simpler way to provide the commit message is to specify the commit message along with the git commit command by using the `-m` option:

```bash
git commit -m "COMMIT MESSAGE" 
```









## Exercise

In this exercise, you will practice the most fundamental Git commands, such as `git add` and `git commit`, and `git status`.

To follow along, log into your development computer and paste the following code block on the command line:

{% code overflow="wrap" %}
```bash
git clone https://github.com/avigewirtz/git_practice.git && cd git_practice && rm -rf .git
```
{% endcode %}

This will copy a directory named _git\_practice_ to your working directory. _git\_practice_ contains 3 files: _hello.c_, _circle1.c_, and _circle2.c_. You can confirm this by invoking `ls -a`.

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 3.56.14 PM (1).png" alt=""><figcaption></figcaption></figure>

Notice that git-practice does not contain a _.git_ directory. This indicates that it is not under Git version control. To begin version controlling _git\_practice_, invoke `git init`:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 3.57.17 PM (1).png" alt=""><figcaption></figcaption></figure>

git\_practice will now have a Git repository. You can verify this by invoking `ls -a` again:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 3.59.00 PM (1).png" alt=""><figcaption></figcaption></figure>

We will now introduce `git status`, which is an extremely useful command that allows you to monitor the state of your worktree. The first time you invoke git status in _git\_practice_, you'll get the following output:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 4.00.05 PM.png" alt=""><figcaption></figcaption></figure>

Any file in the directory that has not previously been staged will be listed under "Untracked files." In our case, since the repository is new, no files in the worktree have been staged yet. This can be illustrated with the following Figure.

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

To get Git to begin tracking the files, you must stage them:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 7.35.05 PM.png" alt=""><figcaption></figcaption></figure>

Notice when we invoke git status again, the files are not listed under "Changes to be commited." That means that they are staged and unmodified. The directory now looks like the following:

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

We can now commit the files with the `git commit` command. When you commit, you also have to provide a commit message. We will do so by supplying the `-m` option:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 7.38.50 PM (1).png" alt=""><figcaption></figcaption></figure>

Now when you invoke git status, you'll get a message letting you know that your working tree is clean--meaning it contains no new content since it was last committed:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 4.05.19 PM.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

## Use Cases

We will not go over some common use cases of staging and committing files.

#### Case 1: Adding a new file

Say you add a new file, file1.txt, to the working directory. In the following example, I add the file with the touch command. If you invoke git status, you'll notice that file1.txt is Untracked:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 4.02.30 PM.png" alt=""><figcaption></figcaption></figure>

#### Case 2: modifying an existing file

Now say you modify the hello.c file by changing "Hello, world" to "Hello, everyone". Invoking Git status, you'll see that _hello.c_ is now classified under "changes not staged for commit."

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 4.03.19 PM.png" alt=""><figcaption></figcaption></figure>

To include the changes in the next commit, you must stage it again. A simple shortcut if you want To add all new or modified files to the staging area, you can use the \* wildcard instead of typing out each filename:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 4.04.08 PM.png" alt=""><figcaption></figcaption></figure>

#### Case 3: Modifying a file after staging it

Now, say you modify hello.c again, by changing "Hello, everyone" back to "Hello, world". If you invoke git status, you will not see two versions of hello.c:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 7.56.28 PM.png" alt=""><figcaption></figcaption></figure>

One of them is listed under "changed to be commits while the other is listed under "changes not staged for commit". The one staged for commit is the "Hello, everyone" version. The "Hello, world version is not staged for commit, since, if you modify a file after staging it, the modified version will not be reflected in the staged version. Rather, if you want the updated version to be included in the next commit, you must stage it again:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 8.05.28 PM.png" alt=""><figcaption></figcaption></figure>

And notice that now the updated version that was previously not staged for commit is staged.

You can now commit, which will save the updated

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 8.06.58 PM.png" alt=""><figcaption></figcaption></figure>

Now say you delete the _file1.txt_ file using the rm command. Although it will be deleted from your working directory, it will not be deleted from your repository. If you invoke git status, you'll notice that file1.txt is listed under "Changes nor staged for commit":

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 8.20.08 PM.png" alt=""><figcaption></figcaption></figure>

Essentially, Git tracks that _file1.txt_ has been deleted, but in order for you to have the deletion reflected in the repository, you need to stage it and then commit it:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 8.22.15 PM.png" alt=""><figcaption></figcaption></figure>

## Summary

* **Staging files**: There are two types of files you need to be staged with the `git add` command: untracked files, and modified files. Untracked files are files that are "new" to Git--that is, they haven't previously been staged. Modified files are files that were updated after they were last staged.
* **Committing files**: The `git commit` command takes the files in the staging area and stores them permanently in your Git repository. Each commit represents a snapshot of your project's state.
* **Status of project files**: The `git status` command lists three categories of files in the working tree:
  1. **Untracked files**: Files in the working directory that were not previously staged (i.e., "new" files).
  2. **Changes not staged for commit**: Files that were modified or deleted since they were last staged.
  3. **Changes to be committed**: Staged files that are ready to be committed.

## Local Git Workflow

The local Git workflow can be summarized with the following diagram:

<figure><img src="../../.gitbook/assets/image (7) (1) (1).png" alt=""><figcaption></figcaption></figure>
