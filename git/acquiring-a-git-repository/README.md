# Local Workflow

In the first part of this tutorial, we'll go over using version control for personal use. All work contained within a single, local repository. We're doing it this way since it's simpler to explain.&#x20;

#### Initializing a Git Repository

Consider the `git_playground` project shown in Figure 2. We'll use it as a running example to demonstrate the basics of the local git workflow.&#x20;

<figure><img src="../../.gitbook/assets/Group 118 (1).png" alt="" width="188"><figcaption></figcaption></figure>

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

<figure><img src="../../.gitbook/assets/Group 133.png" alt="" width="375"><figcaption></figcaption></figure>

#### Saving a Snapshot

It might seem like at this point our work is complete. We created a repository for our project; now, Git will monitor our work and periodically record a snapshot of its current state. This is very much not how it works. Saving snapshots is a manual process. You must explicitly tell Git each time you want it to save a snapshot. This is known as committing. What's more, committing is a two-step process. You must first add the files that you want Git to include in the next commit into an intermediate area known as the index or staging area. Once this is complete, you commit.&#x20;

<figure><img src="../../.gitbook/assets/Group 124.png" alt="" width="375"><figcaption></figcaption></figure>

#### Staging files

To stage the files in the working tree, we invoke `git add` followed by the names of the files or directories we want to stage. If you stage a directory, then all it's contents will be included. Assuming our working directory is \~/git\_playground, we can stage all files in our project by invoking:&#x20;

```bash
git add .
```

And now hello.txt, hi.txt, and bye/bye.txt will be listed in the staging area (Figure 1-1).&#x20;

<figure><img src="../../.gitbook/assets/Group 129 (1).png" alt="" width="375"><figcaption></figcaption></figure>

#### Committing

To save a snapshot of the files in the staging area, we use the `git commit` command. It's general syntax is as follows:&#x20;

```bash
git commit -m "COMMIT_MESSAGE"
```

COMMIT\_MESSAGE is typically a concise, meaningful description of the changes we're committing. This message becomes a part of your commit and helps you (and potentially others) understand the purpose of the commit when reviewing the project's history. In our case, since it's our first commit and we don't have anything meaningful to say, we'll simply write "first commit":

<figure><img src="../../.gitbook/assets/Screenshot 2024-04-04 at 4.47.23 PM.png" alt="" width="563"><figcaption></figcaption></figure>

Our repository now contains a single commit. For simplicity, we'll label this commit "commit 1," but as we'll see soon, commits are identified by a 40-digit hex number.&#x20;

<figure><img src="../../.gitbook/assets/Group 131.png" alt="" width="375"><figcaption><p>Figure 3: Our repository after the first commit.</p></figcaption></figure>

#### Components of a Git Project

Before we delve into recording changes to a repository, let's ensure we understand the components of a Git project. A Git project consists of three components:

* The workspace, or working tree. A working copy of a specific commit, plus any changes.
* The index, or staging area. Contains the files that will be the next commit. Essentially a pseodocommit. An important, often misunderstood thing is that the index does nor merely contain the changes to be committed. It is the next commit. Not just list of filenames, but copy of actual contents from the time you staged. Not just changes, but the entire next commit. As we'll see soon, you only have to manually add changes since last commit, since by dfualy unmodified files are automatically in in the staging area.&#x20;
* Commits. The actual snapshots of your prject stored by git. This is the core of your repository.&#x20;

&#x20;to record changes&#x20;

## Modifying the working tree <a href="#checking_status" id="checking_status"></a>

At this point, if we invoke git status, it'll tell us that our working tree is "clean":

<figure><img src="../../.gitbook/assets/Screenshot 2024-04-04 at 5.10.37 PM.png" alt=""><figcaption></figcaption></figure>

A clean working tree means that our working tree does not contain any new, modified or deleted files. In Git terminology, all the files in our working tree are "unmodified."&#x20;

if anything changes and we want to apply the changes, we will have to add the changes to the index. These modifications include:

* Creating a new file
* Modifying an existing file
* Deleting a file

Let's now make all three modifications to our working. First, let's modify hello.txt by appending "world" to it:

```
echo "world" >> hello.txt
```

Next, let's create a new file named hey.txt, and write "hey" in it:

```
echo "hey" >> hey.txt
```

finally, let's delete the file hi.txt:

```
rm -rf hi.txt
```

Invokig git status, we see that hello.txt is listed as modified, hey.txt as untracked, and hi.txt.&#x20;

Let's now examine the state of our working tree with Git status:&#x20;





The output tells us two things:

1. hello.txt was modified, and the modified version is not staged for commit.&#x20;
2. hey.txt is untracked











A perhaps pedantic but subtle point. Notice how we didn't have to add the unmodified files--hi.txt and bye.txt--to the staging area. We only had to stage hello.txt. This is because unmodified files are automatically in the staging area. This is a subtle point but will. When we invoke git status, it only lists the changes, but not unmodifies files.&#x20;



We see that the newly added file hey.txt is listed as "untracked." What happens is, git looks at the index, and sees no file with the name "hey.txt". (This is different that the previous example of. If a file is not in the index, then then not only is it not part of a previous commit, Git does not even track it. was it never part of In simple terms, an untracked file is one that is not in the staging area.  As we'll see soon, if you modify or delete an untracked file, Git won't&#x20;





{% hint style="info" %}
## When to commit



When working on your own, it’s useful to commit “early and often,” so that you can explore different ideas and make changes freely without worrying about recovering earlier work. Such commits are likely to be somewhat disorganized and have cryptic commit messages, which is fine because they need to be intelligible only to you, and for a short period of time. Once a portion of your work is finished and you’re ready to share it with others, though, you may want to reorganize those commits, to make them well-factored with regard to reusability of the changes being made (especially with software), and to give them mean‐ ingful, well-written commit messages.

The timing for creating commits is up to you, but it's a good practice to commit whenever you've completed a logical chunk of work. For example, if you've implemented a new feature, tested it, and everything works, that's an ideal time to commit. Remember, it's usually better to have smaller, focused commits rather than massive ones that try to cram in many unrelated changes.
{% endhint %}

###

<figure><img src="../../.gitbook/assets/image (7) (1) (1).png" alt=""><figcaption></figcaption></figure>

