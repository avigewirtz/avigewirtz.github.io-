# Local Workflow Fundamentals

In this setion, we'll go over the fundamentals of local git workflow. All operations will be contained with a single repository.&#x20;

#### Setting Up Our Project

Before we dive into using Git, let's set up a simple project that we'll use as a running example throughout this chapter. Follow these steps to create your project.

First, open your terminal and navigate to the directory where you want your project to reside. You can do this by using the cd command:

```bash
cd path/to/your/directory
```

Next, create a new directory named `git_playground` and navigate into it. To do so, the following two commands:

```bash
mkdir git_playground
cd git_playground
```

Let’s now add a few files to our project. We'll create two text files and a subdirectory with another text file. Run the following commands:

```sh
echo "hello" > hello.txt
echo "hi" > hi.txt
mkdir bye
echo "bye" > bye/bye.txt
```

These commands create a hello.txt file containing the text "hello", a hi.txt file with the text "hi", and a bye.txt file with the text "bye" inside a subdirectory named bye.

<figure><img src="../../.gitbook/assets/Group 118 (1).png" alt="" width="188"><figcaption></figcaption></figure>

To ensure the files were created correctly, list the contents of git\_playground with the `ls -R` command. You should see the following output:

```sh
~/git_playground$ ls -R
.    ..    bye    hello.txt    hi.txt

./bye:
.    ..    bye.txt
~/git_playground$ 
```

#### Initializing a Git Repository

With our project set up, the next step is to start tracking it with Git. This is done by initializing a repository in the root directory of our project’s workspace. A repository is a local database that Git will use to store our project’s history. To initialize a repository, run git init. Git will respond by creating a hidden directory named .git in git\_practice (Fig. 15). This directory contains the repository.&#x20;

```bash
~/git_playground$ git init
Initialized empty Git repository in /u/sgewirtz/git_playground/.git/
~/git_playground$
```

You can verify its existence by running `ls -a`:

```bash
~git_playground$ ls -a
.    ..    .git    bye    hello.txt    hi.txt
~/git_playground$ 
```

<figure><img src="../../.gitbook/assets/Group 133.png" alt="" width="375"><figcaption></figcaption></figure>

#### Our first commit

In Git terminology, the files and directories descending from git\_playground make up the working tree. An important thing to understand about git is that it isn't some sort of autosave tool that monitors the working tree and automatically records snapshots of it at different points in time. Whenever you want Git to record a snapshot, you must explicitly tell it to do so. This is known as committing. What's more, committing is a two-step process. First, you must add all (new or modified) files that you want to be included in the next commit into an intermediate area called the index or staging area. Then, you commit the context of the index to the repository. The extra step allows you to easily apply just some of the changes in your working tree (including a subset of changes to a single file), rather than being forced to apply them all at once.

<figure><img src="../../.gitbook/assets/Group 124.png" alt="" width="375"><figcaption></figcaption></figure>

Let’s now stage and commit our project’s files. The command to stage files is git add, which takes one or more files or directories as arguments. If the argument is a directory, it adds all files descending from it.&#x20;

To stage all files in `git_playground`, we run:

```bash
git add .
```

Recall that `.` is a reference to the current directory. Thus, this tells Git to stage all the files descending from `git_playground`. Now, hello.txt, hi.txt, and bye/bye.txt will in the staging area (Figure 1-1). You can print the contents of the staging area with the `git ls-files` command:

<figure><img src="../../.gitbook/assets/Group 129 (1).png" alt="" width="375"><figcaption></figcaption></figure>

To save a snapshot of the contents in the index, we run the `git commit` command. This will open your default text editor and prompt you for a commit message

{% code lineNumbers="true" %}
```

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch main
#
# Initial commit
#
# Changes to be committed:
#       new file:   bye/bye.txt
#       new file:   hello.txt
#       new file:   hi.txt
#
```
{% endcode %}

Add your commit message on line 1 and save the file. The purpose of the commit message is to explain to you or even potentially someone else down the line what changes to the project were introduced by the commit. As such, it should be reasonably descriptive. In our case, because it’s our first commit and we don’t have anything meaningful to say, we’ll just write “first commit”.  Then save the file in the text editor. You should see the following message:

```bash
~/git_playground> git commit
[main (root-commit) f44f93d] first commit
 3 files changed, 4 insertions(+)
 create mode 100644 bye/bye.txt
 create mode 100644 hello.txt
 create mode 100644 hi.txt
~/git_playground> 
```

As an alternative, you can directly add the commit message in the command line using the `-m` option, like so:

```bash
git commit -m "first commit"
```

We’ll use this approach throughout the tutorial.&#x20;

Our repository now contains a single commit (Fig 5). For simplicity, we'll label this commit "commit 1," but as we'll see in the next section, commits are identified by a 40-digit hex number.

<figure><img src="../../.gitbook/assets/Group 131.png" alt="" width="375"><figcaption><p>Figure 3: Our repository after the first commit.</p></figcaption></figure>
