# Local Git Workflow

There are two contexts in which version control is useful: private and public. In the first part of this tutorial, we'll go over using version control for a private project. All work contained within a single repository.&#x20;



* we'll start off by going over the most basic workflow, with no branching, merging.  Then we'll introduce each of the topics one by one. &#x20;

## The big picture

We'll go over a basic workflow that covers the basics core of local workflow:

1. Set up a project by creating a new directory and poulating it with files.&#x20;
2. Initialize a git repository in our new directory.&#x20;
3. Save a snapshot of the files in our directory.&#x20;
4. modify project by and making new commits.&#x20;
   1. Adding new files
   2. Modifying files
   3. deleteing files

Shoud teach you the basics of using the index and commiting.&#x20;



An important command we'll be using the throughout this section is the git status command, which tells you the state of your working tree and index.



## Creating the project

Let's go over each of these steps one by one.&#x20;

```
mkdir playground
cd playground
```

add a few files:

```
echo "hello" > hello.txt 
echo "hi" > hi.txt     
mkdir bye        
echo "bye" > bye/bye.txt
```



<figure><img src="../../.gitbook/assets/Group 118 (1).png" alt="" width="188"><figcaption></figcaption></figure>

## Initializing a repository

Simply invoke `git init` (short for initialize):&#x20;

```bash
~/playground> git init
Initialized empty Git repository in /Users/avigewirtz/playground/.git/
~/playground> 
```

If we invoke ls -l , we'll see that playground has a .git subdirectory:&#x20;

```bash
~/playground> \ls -A
.git    bye    hello.txt    hi.txt
~/playground>
```

<figure><img src="../../.gitbook/assets/Group 133.png" alt="" width="375"><figcaption></figcaption></figure>

The .git subdirectory is a skeleton repository. Essentially empty. We won't get into internals. As we mentioned earlier, .git directory contains two main parts: staging area and commit history. At this point, both are empty.&#x20;

<figure><img src="../../.gitbook/assets/Group 124.png" alt="" width="375"><figcaption></figcaption></figure>

invoke git status.

## Staging our files

First step is adding files we want to be in commit in the staging area. Basic form of stage command is git add:

The filename can be a directory, in which case Git adds all new files and changes to tracked files under that directory.  Whenever you list a directory, all it's descendant are included in the stage as well.

```
git add hello.txt hi.txt bye
```

And now the files will be listed in the staging area:

<figure><img src="../../.gitbook/assets/Group 129 (1).png" alt="" width="375"><figcaption></figcaption></figure>

#### Staging shortcuts

Whenever you list a directory, all it's descendant are included in the stage as well. It naturally follows that if you want to stage all files in the working tree, all you have to do is supply the working tree's root directory (i.e., greetings) as an argument. Recall that "." represents the working directory. Hence, since our working directory is greetings, a shortcut to stage all files is to invoke:

```
git add .
```

In more detail: git add . adds the current directory to the (ini‐ tially empty) index; this includes files as well as directories and their contents, and so on, recursively.&#x20;

### Committing

Committing takes the files in the staging area and creates a snapshot of them. The general form of a Git commit command is as follows:

```bash
git commit -m "COMMIT_MESSAGE"
```

Where COMMIT\_MESSAGE is replaced with a concise, meaningful description of the changes you made. This message becomes a part of your commit and helps you and others understand the purpose of the commit when reviewing the project's history. In our case, since it's our first commit and we don't have anything meaningful to say, we'll simply write "first commit" in the message spot:

<figure><img src="../../.gitbook/assets/Screenshot 2024-04-04 at 4.47.23 PM.png" alt="" width="563"><figcaption></figcaption></figure>

This creates a commit in the repository--for simplicity written as "commit 1"--which stores a snapshot of the current state of our project. We'll go into the details of commits in the next section.

<figure><img src="../../.gitbook/assets/Group 131.png" alt="" width="375"><figcaption><p>Figure 3: Our repository after the first commit.</p></figcaption></figure>

## Modifying the working tree <a href="#checking_status" id="checking_status"></a>

Should be noted that all unmodified files are in index

At this point, we have a "clean" working tree. In other words, no changes have been made to our working tree since the last commit. Such files are called "unmodified." We can check the status of the working tree by invoking `git status`:

<figure><img src="../../.gitbook/assets/Screenshot 2024-04-04 at 5.10.37 PM.png" alt=""><figcaption></figcaption></figure>

If we modify our working tree in any way and we want to record the modified version in our repository, we need to stage the relevant files and commit.&#x20;

### Modifying a file



Let's now make two changes to our project. First, let's modify hello.txt by appending " world" to it:

```
echo "world" >> hello.txt
```

Next, let's create a new file named hey.txt, and write "hey" in it:

```
echo "hey" >> hey.txt
```

Let's now examine the state of our working tree with Git status:&#x20;





The output tells us two things:

1. hello.txt was modified, and the modified version is not staged for commit.&#x20;
2. hey.txt is untracked











A perhaps pedantic but subtle point. Notice how we didn't have to add the unmodified files--hi.txt and bye.txt--to the staging area. We only had to stage hello.txt. This is because unmodified files are automatically in the staging area. This is a subtle point but will. When we invoke git status, it only lists the changes, but not unmodifies files.&#x20;



We see that the newly added file hey.txt is listed as "untracked." What happens is, git looks at the index, and sees no file with the name "hey.txt". (This is different that the previous example of. If a file is not in the index, then then not only is it not part of a previous commit, Git does not even track it. was it never part of In simple terms, an untracked file is one that is not in the staging area.  As we'll see soon, if you modify or delete an untracked file, Git won't&#x20;



DO ADD AND MODIFY TOGETHER, SINCE IT MAKES IT EASIER TO EXPLAIN THE DIFFERENCE



The practical distinction between an untracked and modified file is subtle: Untracked essentially means not Git is not monitoring it's status. As we'll see soon, if you modify or delete an untracked file, Git won't mean that git is not aware of its existence--after all, if that were the case, the file wouldn't appear at all--if it were not, it that git is not monitoring&#x20;









This creates a new subdirectory named `.git` that contains all of your necessary repository files — a Git repository skeleton.&#x20;



<figure><img src="../../.gitbook/assets/Group 112.png" alt="" width="375"><figcaption></figcaption></figure>



All of our&#x20;

<figure><img src="../../.gitbook/assets/Group 114.png" alt="" width="563"><figcaption></figcaption></figure>















###









As we mentioned earlier, a project under git version control can be divided into three components:

* The working tree
* The index
* The repository

The repository essentially consists of commits, or saved snapshots of your project. The staging area consists of a list of new or modified files that are to be included in your next commit. The working tree consists of all the files you're currently working with.&#x20;









{% hint style="success" %}
### **When to Commit**

The timing for creating commits is up to you, but it's a good practice to commit whenever you've completed a logical chunk of work. For example, if you've implemented a new feature, tested it, and everything works, that's an ideal time to commit. Remember, it's usually better to have smaller, focused commits rather than massive ones that try to cram in many unrelated changes.
{% endhint %}















\










## Worktree

Every (non-bare) Git repository has an associated _worktree_ (also called _working tree_). The worktree is essentially synonymous with the working directory. It is the area you do all of your project development in.

The worktree is distinct from the repository. The repository serves as the area where the project's history is stored. You don't develop in the repository. Instead, you develop in the worktree, and whenever you are ready to save a snapshot of your project, you tell Git to copy the changes from the worktree into the repository. This is called _committing_.

## Commits

Commits are the foundation of a Git repository. Each commit represents a snapshot of the project at a certain point in time. This idea is illustrated in the Figure below, where each commit is represented as a version of the project.

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
