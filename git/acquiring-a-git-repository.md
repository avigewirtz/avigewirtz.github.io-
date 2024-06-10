# Local Workflow

In the first part of this tutorial, we'll go over using version control for personal use. All work contained within a single, local repository. We're doing it this way since it's simpler to explain.

#### Setting Up Our Project

Before we dive into using Git, let's set up a simple project that we'll use as a running example throughout this tutorial. Follow these steps to create your project.

First, open your terminal and navigate to the directory where you want your project to reside. Then, create a new directory for the project by running the following commands:

```bash
mkdir git_playground
cd git_playground
```

This creates a new directory called `git_playground` and moves you into it.

Next, let's add a few files to our project. We'll create two text files and a subdirectory with another text file. Run the following commands:

```sh
echo "hello" > hello.txt
echo "hi" > hi.txt
mkdir bye
echo "bye" > bye/bye.txt
```

These commands create a `hello.txt` file containing the text "hello", a `hi.txt` file with the text "hi", and a `bye.txt` file with the text "bye" inside a subdirectory named `bye`.

<figure><img src="../.gitbook/assets/Group 118 (1).png" alt="" width="188"><figcaption></figcaption></figure>

To ensure the files were created correctly, list the contents of git\_playground with the `ls -R` command. You should see the following output:

```sh
~/git_playground$ ls -R
.    ..    bye    hello.txt    hi.txt

./bye:
.    ..    bye.txt
~/git_playground$ 
```

#### Initializing a Git Repository

With our project set up, the next step is to initialize a Git repository in it. A repository is essentially a database where git stores the history of our project.

To initialize a Git repository, run `git init` (short for initialize):

```bash
~/git_playground$ git init
Initialized empty Git repository in /u/sgewirtz/git_playground/.git/
~/git_playground$
```

Git creates a hidden directory named `.git` in your project directory. This directory contains the repository. You can verify its existence by running `ls -a`:

```bash
~git_playground$ ls -a
.    ..    .git    bye    hello.txt    hi.txt
~/git_playground$ 
```

<figure><img src="../.gitbook/assets/Group 133.png" alt="" width="375"><figcaption></figcaption></figure>

#### Our first commit

In Git terminology, the files and directories descending from git\_playground make up the working tree. An important thing to understand about git is that it isn't some sort of autosave tool that constantly monitors our work and periodically saves snapshots.  You must explicitly tell Git each time you want it to save a snapshot. This is known as committing. What's more, committing is a two-step process. First, you add the changes to an intermediate area called the _index_ or _staging area_, then commit those changes to the repository. The extra step allows you to easily apply just some of the changes in your working tree (including a subset of changes to a single file), rather than being forced to apply them all at once.&#x20;

<figure><img src="../.gitbook/assets/Group 124.png" alt="" width="375"><figcaption></figcaption></figure>

To stage the files in the working tree, we invoke `git add` followed by the names of the files and directories we want to stage. If you stage a directory, then all it's contents will be included. Assuming our working directory is \~/git\_playground, we can stage all files in our project by invoking:

```bash
git add .
```

And now hello.txt, hi.txt, and bye/bye.txt will be added to the staging area (Figure 1-1). . You can print the list of files in the staging area with the git ls command.

<figure><img src="../.gitbook/assets/Group 129 (1).png" alt="" width="375"><figcaption></figcaption></figure>

To save a snapshot of the files in the staging area, we use the `git commit` command. It's general syntax is as follows:

```bash
git commit -m "COMMIT_MESSAGE"
```

COMMIT\_MESSAGE is typically a concise, meaningful description of the changes we're committing. This message becomes a part of your commit and helps you (and potentially others) understand the purpose of the commit when reviewing the project's history. In our case, since it's our first commit and we don't have anything meaningful to say, we'll simply write "first commit":

<figure><img src="../.gitbook/assets/Screenshot 2024-04-04 at 4.47.23 PM.png" alt="" width="563"><figcaption></figcaption></figure>

Our repository now contains a single commit. For simplicity, we'll label this commit "commit 1," but as we'll see soon, commits are identified by a 40-digit hex number.

<figure><img src="../.gitbook/assets/Group 131.png" alt="" width="375"><figcaption><p>Figure 3: Our repository after the first commit.</p></figcaption></figure>



#### Components of a Git Project

Before we delve into the details of recording changes to a repository, let's ensure we understand the components of a Git project. As our example has hopefully shown, a Git project consists of three main components:

* The working tree. A working copy of a specific commit, plus any changes.
* The index, or staging area. Contains the files that will be the next commit. Essentially a pseudocommit. A few important, often misunderstood points about the index:
  * Not just modified files, but all files. It is the next commit.&#x20;
  * Not just list of files to be included in next commit, but copy of actual contents from the time you staged.&#x20;
* Commits.  At its core, a commit represents a snapshot of the entire project at a specific point in time. Additionally, a commit also contains the following metadata that provides context about the commit:&#x20;
  * The commit author's name and email.
  * The time and date the commit was made
  * The commit message. The message git requires you to provide when making a commit. It should be descriptive, explaining the purpose of the changes.
  * A pointer to its parent commits.

#### Recording Changes To Our Repository <a href="#checking_status" id="checking_status"></a>

Now that we understand the components of a Git repository, let's get into the nitty gritty of recording changes to the repository. An important command we'll be using is git status. Git status compares the working tree to the index and the index to the latest commit and reports any changes. At this point, if we invoke git status, it'll tell us that our working tree is "clean":

<figure><img src="../.gitbook/assets/Screenshot 2024-04-04 at 5.10.37 PM.png" alt=""><figcaption></figcaption></figure>

In simple terms, this means that working tree, index, and latest commit are in sync.

Suppose we modify hello.txt by appending "world" to it:

```
echo "world" >> hello.txt
```

invoking git status, we'll now see that hello.txt is listed as modified:

git compares hello.txt in our working tree to the version of hello.txt in the index and sees that they're different.

scenario 2: modifying a file after staging it

let's now modify hello.txt again and stage it, but this time, before committing it, we modify it another time.

scenario 3:

suppose we now create a new file in our working tree, which we'll call hey.txt.

git status, we see it listed as untracked.

Next, let's create a new file named hey.txt, and write "hey" in it:

```
echo "hey" >> hey.txt
```

finally, let's delete the file hi.txt:

```
rm -rf hi.txt
```

Invokig git status, we see that hello.txt is listed as modified, hey.txt as untracked, and hi.txt.

We see that the newly added file hey.txt is listed as "untracked." What happens is, git looks at the index, and sees no file with the name "hey.txt". (This is different that the previous example of. If a file is not in the index, then then not only is it not part of a previous commit, Git does not even track it. was it never part of In simple terms, an untracked file is one that is not in the staging area. As we'll see soon, if you modify or delete an untracked file, Git won't
