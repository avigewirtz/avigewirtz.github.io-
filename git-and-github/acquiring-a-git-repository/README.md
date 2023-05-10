# Git Workflow

## Worktree

Every (non-bare) Git repository has an associated _worktree_ (also called _working tree_). The worktree is essentially synonymous with the working directory. It is the area you do all of your project development in.&#x20;

The worktree is distinct from the repository. The repository serves as the area where the project's history is stored. You don't develop in the repository. Instead, you develop in the worktree, and whenever you are ready to save a snapshot of your project, you tell Git to copy the changes from the worktree into the repository. This is called _committing_.&#x20;

## Commits

Commits are the foundation of a Git repository. Each commit represents a snapshot of the project at a certain point in time. This idea is illustrated in the Figure below, where each commit is represented as a version of the project.&#x20;

<figure><img src="../../.gitbook/assets/snapshots-2.png" alt=""><figcaption><p>Courtesy of Git-SCM</p></figcaption></figure>

Each commit has a unique identifier, which is used by Git to reference it. Git records important information along with each commit, such as the timestamp of the commit, the author's name and email address, as well as the commit message, which is a short message provided by the commit author that serves to document the commit.&#x20;

There are two important things to recognize with how commits work in Git:

1. **All commits must be done manually**. That is, Git does not automatically commit anything from the worktree. Consequently, whenever you create a new Git repository, the repository will initially be empty--that is, the files previously present in the directory, which are now in the worktree, will not automatically be committed to the Git repository. In fact, they will not even be _tracked_, which we'll cover soon. Similarly, if you modify files in the worktree, the modified version will not automatically be committed.
2. **Committing is a two-step process**. Before changes can be committed from the worktree to the repository, they must be added to an intermediate area called the _index_ or _staging area_. In this step, you selectively choose the changes you want to include in the next commit. This allows you to review, group, or organize the changes before you save them to the repository. When you commit changes, you commit the changes that are in the staging area only.&#x20;

### Staging files

There are two types of files that have to be staged: untracked files and modified files. Untracked files are new files--that is, files that were not previously in the repository. Modified files, on the other hand, are those that were previously in the repository but whose contents have since been modified.&#x20;

Staging is accomplished with the `git add` command, where you specify each of the untracked or modified files you want to stage:&#x20;

```bash
git add FILE(S)
```

If you want to stage all relevant files, you can save time by using the `*` [wildcard](../../bash/useful-command-line-features.md#wildcards):

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

In this exercise, you will practice the most fundamental Git commands, such as `git add` and `git commit`, and `git status`.&#x20;

To follow along, log into your development computer and paste the following code block on the command line:

{% code overflow="wrap" %}
```bash
git clone https://github.com/avigewirtz/git_practice.git && cd git_practice && rm -rf .git
```
{% endcode %}

This will copy a directory named _git\_practice_ to your working directory. _git\_practice_ contains 3 files: _hello.c_, _circle1.c_, and _circle2.c_. You can confirm this by invoking `ls -a`.

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 3.56.14 PM.png" alt=""><figcaption></figcaption></figure>

Notice that git-practice does not contain a _.git_ directory. This indicates that it is not under Git version control. To begin version controlling _git\_practice_, invoke `git init`:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 3.57.17 PM.png" alt=""><figcaption></figcaption></figure>

git\_practice will now have a Git repository. You can verify this by invoking `ls -a` again:&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 3.59.00 PM.png" alt=""><figcaption></figcaption></figure>

We will now introduce `git status`, which is an extremely useful command that allows you to monitor the state of your worktree. The first time you invoke git status in _git\_practice_, you'll get the following output:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 4.00.05 PM (1).png" alt=""><figcaption></figcaption></figure>

Any file in the directory that has not previously been staged will be listed under "Untracked files." In our case, since the repository is new, no files in the worktree have been staged yet. This can be illustrated with the following Figure.

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

To get Git to begin tracking the files, you must stage them:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 7.35.05 PM.png" alt=""><figcaption></figcaption></figure>

Notice when we invoke git status again, the files are not listed under "Changes to be commited." That means that they are staged and unmodified. The directory now looks like the following:

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

We can now commit the files with the `git commit` command. When you commit, you also have to provide a commit message. We will do so by supplying the `-m` option:&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 7.38.50 PM.png" alt=""><figcaption></figcaption></figure>

Now when you invoke git status, you'll get a message letting you know that your working tree is clean--meaning it contains no new content since it was last committed:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 7.39.56 PM.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

## Use Cases

We will not go over some common use cases of staging and committing files.

#### Case 1: Adding a new file

Say you add a new file, file1.txt, to the working directory. In the following example, I add the file with the touch command. If you invoke git status, you'll notice that file1.txt is Untracked:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 4.02.30 PM.png" alt=""><figcaption></figcaption></figure>

#### Case 2: modifying an existing file

Now say you modify the hello.c file by changing "Hello, world" to "Hello, everyone". Invoking Git status, you'll see that _hello.c_ is now classified under "changes not staged for commit."&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 4.03.19 PM.png" alt=""><figcaption></figcaption></figure>

To include the changes in the next commit, you must stage it again. A simple shortcut if you want To add all new or modified files to the staging area, you can use the \* wildcard instead of typing out each filename:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 4.04.08 PM.png" alt=""><figcaption></figcaption></figure>

#### Case 3: Modifying a file after staging it

Now, say you modify hello.c again, by changing "Hello, everyone" back to "Hello, world". If you invoke git status, you will not see two versions of hello.c:&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 7.56.28 PM.png" alt=""><figcaption></figcaption></figure>

One of them is listed under "changed to be commits while the other is listed under "changes not staged for commit". The one staged for commit is the "Hello, everyone" version. The "Hello, world version is not staged for commit, since, if you modify a file after staging it, the modified version will not be reflected in the staged version. Rather, if you want the updated version to be included in the next commit, you must stage it again:&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 8.05.28 PM.png" alt=""><figcaption></figcaption></figure>

And notice that now the updated version that was previously not staged for commit is staged.&#x20;

You can now commit, which will save the updated&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 8.06.58 PM.png" alt=""><figcaption></figcaption></figure>

Now say you delete the _file1.txt_ file using the rm command. Although it will be deleted from your working directory, it will not be deleted from your repository. If you invoke git status, you'll notice that file1.txt is listed under "Changes nor staged for commit":

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 8.20.08 PM.png" alt=""><figcaption></figcaption></figure>

Essentially, Git tracks that _file1.txt_ has been deleted, but in order for you to have the deletion reflected in the repository, you need to stage it and then commit it:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 8.22.15 PM.png" alt=""><figcaption></figcaption></figure>

## Summary

* **Staging files**: There are two types of files you need to be staged with the `git add` command: untracked files, and modified files. Untracked files are files that are "new" to Git--that is, they haven't previously been staged. Modified files are files that were updated after they were last staged.&#x20;
* **Committing files**: The `git commit` command takes the files in the staging area and stores them permanently in your Git repository. Each commit represents a snapshot of your project's state.
* **Status of project files**: The `git status` command lists three categories of files in the working tree:
  1. **Untracked files**: Files in the working directory that were not previously staged (i.e., "new" files).&#x20;
  2. **Changes not staged for commit**: Files that were modified or deleted since they were last staged.&#x20;
  3. **Changes to be committed**: Staged files that are ready to be committed.

## Local Git Workflow

The local Git workflow can be summarized with the following diagram:

<figure><img src="../../.gitbook/assets/image (7) (1) (1).png" alt=""><figcaption></figcaption></figure>
