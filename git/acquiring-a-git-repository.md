# Local Workflow

In the first part of this tutorial, we'll go over using version control for personal use. All work contained within a single, local repository. We're doing it this way since it's simpler to explain.&#x20;

#### Initializing a Git Repository

Consider the `git_playground` project shown in Figure 2. We'll use it as a running example to demonstrate the basics of the local git workflow.&#x20;

<figure><img src="../.gitbook/assets/Group 118 (1).png" alt="" width="188"><figcaption></figcaption></figure>

The first step to version controlling `git_playground` with Git is to initialize a local database or _repository_ where git will store it's history. To do so, we first cd into git\_playground:&#x20;

```
cd ~/git_playground
```

Then, we run `git init` (short for initialize):

```bash
~/git_playground> git init
Initialized empty Git repository in /u/sgewirtz/git_playground/.git/
~/git_playground> 
```

git creates a `.git` directory in the root directory of our project's workspace (Figure 15), which contains the git repository.

<figure><img src="../.gitbook/assets/Group 133.png" alt="" width="375"><figcaption></figcaption></figure>

#### Our first commit

It might seem like at this point our work is complete. We created a repository for our project; now, Git will monitor our work and periodically record a snapshot of its current state. This is very much not how it works. Saving snapshots is a manual process. You must explicitly tell Git each time you want it to save a snapshot. This is known as committing. What's more, committing is a two-step process. you add the changes to a staging area called the _index_ or _staging area_, then commit those changes to the repository. The extra step allows you to easily apply just some of the changes in your current working files (including a subset of changes to a single file), rather than being forced to apply them all at once, or undoing some of those changes yourself before committing and then redoing them by hand. This encourages splitting changes up into better organized, more coherent and reusable sets.

<figure><img src="../.gitbook/assets/Group 124.png" alt="" width="375"><figcaption></figcaption></figure>

To stage the files in the working tree, we invoke `git add` followed by the names of the files or directories we want to stage. If you stage a directory, then all it's contents will be included. Assuming our working directory is \~/git\_playground, we can stage all files in our project by invoking:&#x20;

```bash
git add .
```

And now hello.txt, hi.txt, and bye/bye.txt will be listed in the staging area (Figure 1-1).&#x20;

<figure><img src="../.gitbook/assets/Group 129 (1).png" alt="" width="375"><figcaption></figcaption></figure>

To save a snapshot of the files in the staging area, we use the `git commit` command. It's general syntax is as follows:&#x20;

```bash
git commit -m "COMMIT_MESSAGE"
```

COMMIT\_MESSAGE is typically a concise, meaningful description of the changes we're committing. This message becomes a part of your commit and helps you (and potentially others) understand the purpose of the commit when reviewing the project's history. In our case, since it's our first commit and we don't have anything meaningful to say, we'll simply write "first commit":

<figure><img src="../.gitbook/assets/Screenshot 2024-04-04 at 4.47.23 PM.png" alt="" width="563"><figcaption></figcaption></figure>

Our repository now contains a single commit. For simplicity, we'll label this commit "commit 1," but as we'll see soon, commits are identified by a 40-digit hex number.&#x20;

<figure><img src="../.gitbook/assets/Group 131.png" alt="" width="375"><figcaption><p>Figure 3: Our repository after the first commit.</p></figcaption></figure>

#### Components of a Git Project

Before we delve into the details of recording changes to a repository, let's ensure we understand the components of a Git project. As our example has hopefully shown, a Git project consists of three main components:

* The workspace, or working tree. A working copy of a specific commit, plus any changes.
* The index, or staging area. Contains the files that will be the next commit. Essentially a pseudocommit. A few important, often misunderstood points about the index:
  * Not just modified files, but all files. It is the next commit.&#x20;
  * Not just list of files to be included in next commit, but copy of actual contents from the time you staged.&#x20;
* Commits. The actual snapshots of your prject stored by git. This is the core of your repository.&#x20;

&#x20;&#x20;

#### Recording Changes To Our Repository <a href="#checking_status" id="checking_status"></a>

An important command we'll be using is git status. At this point, if we invoke git status, it'll tell us that our working tree is "clean":

<figure><img src="../.gitbook/assets/Screenshot 2024-04-04 at 5.10.37 PM.png" alt=""><figcaption></figcaption></figure>

In simple terms, this means that working tree, index, and latest commit are in sync.&#x20;

Suppose we modify hello.txt by appending "world" to it:

```
echo "world" >> hello.txt
```

invoking git status, we'll now see that hello.txt is listed as modified:



Next, let's create a new file named hey.txt, and write "hey" in it:

```
echo "hey" >> hey.txt
```

finally, let's delete the file hi.txt:

```
rm -rf hi.txt
```

Invokig git status, we see that hello.txt is listed as modified, hey.txt as untracked, and hi.txt.&#x20;

We see that the newly added file hey.txt is listed as "untracked." What happens is, git looks at the index, and sees no file with the name "hey.txt". (This is different that the previous example of. If a file is not in the index, then then not only is it not part of a previous commit, Git does not even track it. was it never part of In simple terms, an untracked file is one that is not in the staging area.  As we'll see soon, if you modify or delete an untracked file, Git won't&#x20;
