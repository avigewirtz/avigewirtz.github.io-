# Local Workflow

In the first part of this tutorial, we'll go over using version control for personal use. All work contained within a single, local repository. We're doing it this way since it's simpler to explain.

#### Setting Up Our Project

Before we dive into using Git, let's set up a simple project that we'll use as a running example throughout this tutorial. Follow these steps to create your project.

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

With our project set up, the next step is to start tracking it with Git. To do so, we initialize a repository in the root directory of our project’s workspace. A repository is a local database that Git will use to store our project’s history. To initialize a repository, run git init. Git will respond by creating a hidden directory named .git in git\_practice (Fig. 15). This directory contains the repository.&#x20;

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

<figure><img src="../.gitbook/assets/Group 133.png" alt="" width="375"><figcaption></figcaption></figure>

#### Our first commit

In Git terminology, the files and directories descending from git\_playground make up the working tree. An important thing to understand about git is that it isn't some sort of autosave tool that monitors the working tree and automatically records snapshots of it at different points in time. Whenever you want Git to record a snapshot, you must explicitly tell it to do so. This is known as committing. What's more, committing is a two-step process. First, you must add all (new or modified) files that you want to be included in the next commit into an intermediate area called the index or staging area. Then, you commit the context of the index to the repository. The extra step allows you to easily apply just some of the changes in your working tree (including a subset of changes to a single file), rather than being forced to apply them all at once.

<figure><img src="../.gitbook/assets/Group 124.png" alt="" width="375"><figcaption></figcaption></figure>

Let’s now stage and commit our project’s files. The command to stage files is git add, which takes one or more files or directories as arguments. If the argument is a directory, it adds all files descending from it.&#x20;

To stage all files in `git_playground`, we run:

```bash
git add .
```

Recall that `.` is a reference to the current directory. Thus, this tells Git to stage all the files descending from `git_playground`. Now, hello.txt, hi.txt, and bye/bye.txt will in the staging area (Figure 1-1). You can print the contents of the staging area with the `git ls-files` command:

<figure><img src="../.gitbook/assets/Group 129 (1).png" alt="" width="375"><figcaption></figcaption></figure>

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

<figure><img src="../.gitbook/assets/Group 131.png" alt="" width="375"><figcaption><p>Figure 3: Our repository after the first commit.</p></figcaption></figure>



An important thing to recognize is that after a commit, the index isn't wiped clean. All the files we just committed remain in the index. You can verify this by running git ls-files:

```bash
git ls-files
```

For this reason, in subsequent we only need to add new or modified files. We don't need to add unmodified files, since they're already in the index from the previous commit.&#x20;

#### Components of a Git Project

Before we delve into the details of recording changes to a repository, let's ensure we understand the components of a Git project. As our example has hopefully shown, a Git project consists of three main components:

* The working tree. A working copy of a specific commit, plus any changes.
* The index, or staging area. Contains the files that will be the next commit. Essentially a pseudocommit. A few important, often misunderstood points about the index:
  * Not just changes, but entire next commit. As we'll see below, we only need to explicitly add new or modified files, since unmodified files are automatically in index.&#x20;
  * When you add files to the index, git does more than just record the filenames in the index. It creates a copy of the files at the time you added it to the index. Index contains pointer to copy of each file. For simplicity, we'll avoid getting into git internals and assume actual contents are stored in index. The important thing to understand is that adding a file to the index creates a copy, which is what the index looks at. It does not look at the version of the file in your working tree.&#x20;
* The commit history. The actual snapshots of the project at various points in the time. This is the core of the repository. Again, the commit itself does not store the contents of the snapshot, but a pointer to the contents. For simplicity, however, we'll assume contents of snapshot are stored in commit.  Additionally, a commit also contains the following metadata that provides context about the commit:&#x20;
  * The commit author's name and email.
  * The time and date the commit was made.
  * The commit message.&#x20;
  * A pointer to its parent commit(s).

#### Recording Changes To Our Repository <a href="#checking_status" id="checking_status"></a>

Now that we understand the components of a Git project, let's dive into the details of recording changes to the repository. One of the key commands we'll be using is `git status`. This command compares the working tree to the index and the index to the latest commit, reporting any changes. At this point, if we invoke `git status`, it'll tell us that our working tree is "clean":

<figure><img src="../.gitbook/assets/Screenshot 2024-04-04 at 5.10.37 PM.png" alt=""><figcaption></figcaption></figure>

There are four common scenarios that can make our working tree "dirty": modifying a file, adding a new file, deleting a file, and renaming a file. Let's explore each one.

**Modifying a File**

Suppose we modify `hello.txt` by appending "world" to it:

```
echo "world" >> hello.txt
```

Now, let's check the status:

```bash
~/git_playground$ git status
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   hello.txt

no changes added to commit (use "git add" and/or "git commit -a")
~/git_playground$
```

We see that `hello.txt` is listed under "Changes not staged for commit" as "modified." Git compares `hello.txt` in our working tree to the version of `hello.txt` in the index and sees that they're different. To include the modified version in our next commit, we need to add it to the index:

```bash
git add hello.txt
```

Let's check the status again:

```bash
~/git_playground$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   hello.txt

~/git_playground$
```

Now `hello.txt` is still listed as "modified," but this time under "Changes to be committed." Git compares the version of `hello.txt` in the index to the version in the latest commit and reports that they're different. To save a snapshot of the contents in the index, we run:

```
~/git_playground$ git commit -m "appended 'world' to hello.txt"
[main 66ee698] appended 'world' to hello.txt
 1 file changed, 1 insertion(+)
~/git_playground$ 
```

**Modifying a Staged File**

Let's say we now modify `hi.txt` and stage it:

```
~/git_playground$ echo "there" >> hi.txt
~/git_playground$ git add hi.txt 
```

When we check the status, we'll see `hi.txt` listed as "modified" under "Changes to be committed":

```
~/git_playground$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   hi.txt

~/git_playground$ 
```

Now, suppose that instead of committing, we modify `hi.txt` again, this time appending "world" to it:

```
~/git_playground$ echo "world" >> hi.txt
```

When we check the status again, we see something interesting. `hi.txt` is listed as modified under both "Changes to be committed" and "Changes not staged for commit":

```git
~/git_playground$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   hi.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   hi.txt

~/git_playground$
```

What's going on here? If you're following what we discussed earlier about Git copying the file's contents when you stage the file, this makes sense. The version of `hi.txt` that was staged first contains "there," but the working tree version now contains "there" and "world." Git tracks both versions separately: the staged version and the working tree version.

**Adding a New File**

Let's say we want to add a new file to our project. We'll create a new file called `greeting.txt`:

```bash
echo "hello, world" > greeting.txt
```

Now, let's check the status:

```bash
~/git_playground$ git status
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	greeting.txt

nothing added to commit but untracked files present (use "git add" to track)
~/git_playground$
```

We see that `greeting.txt` is listed under "Untracked files." This means Git knows about the file, but it’s not being tracked yet. To understand this better, let's compare it to a modified file.

When a file is **modified**, a version of it already exists in the index. When you change this file, Git compares the current version in your working tree to the version in the index and reports that the file is "modified."

With an **untracked** file like `greeting.txt`, however, Git doesn’t have a reference for this file in the index. This means Git isn’t monitoring its contents. If you modify an untracked file, Git won't know about the changes because it’s not tracking the file’s contents yet.

To start tracking `greeting.txt` and include it in our next commit, we need to add it to the index:

```bash
git add greeting.txt
```

Now, let's check the status again:

```bash
~/git_playground$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   greeting.txt
~/git_playground$
```

We see that `greeting.txt` is now listed under "Changes to be committed" as a "new file." This means it has been added to the index and will be included in the next commit. To save a snapshot of the index, including our new file, we run:

```bash
git commit -m "added greeting.txt with a friendly message"
```

You should see a message like this:

```bash
[main 5d41402] added greeting.txt with a friendly message
 1 file changed, 1 insertion(+)
 create mode 100644 greeting.txt
~/git_playground$
```

Now, our repository includes the new file `greeting.txt`, and the commit history has been updated to reflect this addition.

**Modifying Another New File After Staging**

Let's create another new file called `farewell.txt` and add some text to it:

```bash
echo "goodbye, world" > farewell.txt
```

Now, let's check the status:

```bash
~/git_playground$ git status
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	farewell.txt

nothing added to commit but untracked files present (use "git add" to track)
~/git_playground$
```

We see that `farewell.txt` is listed under "Untracked files." Let's add it to the index:

```bash
git add farewell.txt
```

Now, let's check the status again:

```bash
~/git_playground$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   farewell.txt
~/git_playground$
```

Now `farewell.txt` is listed under "Changes to be committed" as a "new file." This means it has been added to the index and will be included in the next commit.

What happens if we modify `farewell.txt` after adding it to the index? Let's append more text to it:

```bash
echo "see you later" >> farewell.txt
```

Now, let's check the status again:

```bash
~/git_playground$ git status
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   farewell.txt

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   farewell.txt

~/git_playground$
```

We see that `farewell.txt` is now listed under both "Changes not staged for commit" and "Changes to be committed." This is because Git compares the current version of `farewell.txt` in the working tree to the version in the index and sees that they are different.

To include the modified version of `farewell.txt` in our next commit, we need to add it to the index again:

```bash
git add farewell.txt
```

Now, let's check the status again:

```bash
~/git_playground$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   farewell.txt
~/git_playground$
```

Now `farewell.txt` is listed under "Changes to be committed" as "modified." This means the updated version is now staged for the next commit.

To save a snapshot of the updated index, including our modified file, we run:

```bash
git commit -m "appended 'see you later' to farewell.txt"
```

You should see a message like this:

```bash
[main 8b6b5c1] appended 'see you later' to farewell.txt
 1 file changed, 1 insertion(+)
~/git_playground$
```

By understanding how to add new files, modify them, and track these changes in Git, you can effectively manage your project’s history and ensure all important changes are recorded accurately.

**Deleting a File**

Now, let's see what happens when we delete a file in our project. We'll delete the `hi.txt` file.

First, let's check the current status to see the files in our project:

```bash
~/git_playground$ ls
bye  greeting.txt  hello.txt  hi.txt  farewell.txt
```

To delete `hi.txt`, we can use the `rm` (remove) command:

```bash
rm hi.txt
```

Now, let's check the status again:

```bash
~/git_playground$ git status
On branch main
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	deleted:    hi.txt

no changes added to commit (use "git add" and/or "git commit -a")
~/git_playground$
```

We see that `hi.txt` is listed under "Changes not staged for commit" as "deleted." What does this mean? Git compares the working tree to the index. Even though we deleted `hi.txt` from the working tree, it still exists in the index. This discrepancy is what Git reports as a "deleted" file.

If we don't stage the deleted file, it won't be included in the next commit. This makes sense if you understand that the index maintains an independent copy of the file—the version at the time you staged it. The index isn't automatically updated to reflect the working tree changes unless you explicitly stage those changes.

To stage the deletion of `hi.txt`, we need to use the `git rm` command. This tells Git to track the file deletion:

```bash
git rm hi.txt
```

Alternatively, if we had used `git rm hi.txt` instead of `rm hi.txt`, it would have deleted the file and staged the deletion in one step. Let's demonstrate this by recreating and deleting the file using `git rm`:

First, recreate `hi.txt`:

```bash
echo "hi" > hi.txt
git add hi.txt
git commit -m "recreated hi.txt"
```

Now, let's use `git rm` to remove and stage the deletion in one step:

```bash
git rm hi.txt
```

Let's check the status again:

```bash
~/git_playground$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	deleted:    hi.txt
~/git_playground$
```

Now `hi.txt` is listed under "Changes to be committed" as "deleted." This means the deletion has been staged and will be included in the next commit.

To save a snapshot of the index, including the deletion of `hi.txt`, we run:

```bash
git commit -m "deleted hi.txt using git rm"
```

You should see a message like this:

```bash
[main d47f1c3] deleted hi.txt using git rm
 1 file changed, 0 insertions(+), 0 deletions(-)
 delete mode 100644 hi.txt
~/git_playground$
```

Now, our repository has been updated to reflect the deletion of `hi.txt`. By understanding how to delete files and track these changes in Git, you can manage your project’s history effectively, ensuring that all important changes, including deletions, are recorded accurately.

**Renaming a File**

Let's see what happens when we rename a file in our project. We'll rename the `hello.txt` file to `greetings.txt`.

First, let's check the current status to see the files in our project:

```bash
~/git_playground$ ls
bye  farewell.txt  greeting.txt  hello.txt
```

To rename `hello.txt` to `greetings.txt`, we can use the `mv` (move) command:

```bash
mv hello.txt greetings.txt
```

Now, let's check the status:

```bash
~/git_playground$ git status
On branch main
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	renamed:    hello.txt -> greetings.txt

no changes added to commit (use "git add" and/or "git commit -a")
~/git_playground$
```

We see that the file is listed under "Changes not staged for commit" as "renamed: hello.txt -> greetings.txt." This means Git has detected the renaming of the file but hasn't staged the change yet.

To stage the renaming of `hello.txt` to `greetings.txt`, we use the `git add` command:

```bash
git add greetings.txt
```

Alternatively, we can use `git mv` instead of `mv` to rename the file and stage the change in one step:

```bash
git mv hello.txt greetings.txt
```

Let's undo the previous rename and use `git mv` for demonstration:

First, undo the previous rename:

```bash
mv greetings.txt hello.txt
git add hello.txt
git commit -m "restored hello.txt"
```

Now, let's use `git mv` to rename and stage the change in one step:

```bash
git mv hello.txt greetings.txt
```

Let's check the status again:

```bash
~/git_playground$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	renamed:    hello.txt -> greetings.txt
~/git_playground$
```

Now, `hello.txt` is listed under "Changes to be committed" as "renamed: hello.txt -> greetings.txt." This means the renaming has been staged and will be included in the next commit.

To save a snapshot of the index, including the renaming of the file, we run:

```bash
git commit -m "renamed hello.txt to greetings.txt"
```

You should see a message like this:

```bash
[main e7d1c8a] renamed hello.txt to greetings.txt
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename hello.txt => greetings.txt (100%)
~/git_playground$
```

Now, our repository has been updated to reflect the renaming of `hello.txt` to `greetings.txt`. By understanding how to rename files and track these changes in Git, you can manage your project’s history effectively, ensuring that all important changes, including renames, are recorded accurately.
