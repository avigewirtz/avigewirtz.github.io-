# Branching

A Git branch is the simplest thing possible: a pointer to a commit, as a ref. Or rather, that is its implementation; the branch itself is defined as all points reachable in the commit graph from the named commit (the “tip” of the branch). The special ref HEAD determines what branch you are on; if HEAD is a symbolic ref for an existing branch, then you are “on” that branch. If, on the other hand, HEAD is a simple ref directly naming a commit by its SHA-1 ID, then you are not “on” any branch, but rather in “detached HEAD” mode, which happens when you check out some earlier commit to examine. Let’s see:



The labels on the right side of this picture—master, topic, and release—denote “branches.” The branch name refers to the latest commit on that branch; here, commits F, 4, and Z, respectively, are called the “tip” of the branch. The branch itself is defined as the collection of all commits in the graph that are reachable from the tip by following the parent arrows backward along the history. Here, the branches are:

* release = {A, B, C, X, Y, Z}
* master = {A, B, C, D, E, F, 1, 2}

Overview | 3

• topic = {A, B, 1, 2, 3, 4}

Note that branches can overlap; here, commits 1 and 2 are on both the master and topic branches, and commits A and B are on all three branches. Usually, you are “on” a branch, looking at the content corresponding to the tip commit on that branch. When you change some files and add a new commit containing the changes (called “committing to the repository”), the branch name advances to the new commit, which in turn points to the old commit as its sole parent; this is the way branches move for‐ ward. From time to time, you will tell Git to “merge” several branches (most often two, but there can be more), tying them together as at commit E in Figure 1-1. The same branches can be merged repeatedly over time, showing that they continued to progress separately while you periodically combined their contents.

The first branch in a new repository is named master by default, and it’s customary to use that name if there is only one branch in the repository, or for the branch that contains the main line of development (if that makes sense for your project). You are not required to do so, however, and there is nothing special about the name “master” apart from convention, and its use as a default by some commands.





A branch evolves over time; thus, if you are on the branch mas‐ ter and make a commit, Git does the following:

1. Creates a new commit with your changes to the repository content
2. Makes the commit at the current tip of the master branch the parent of the new commit
3. Adds the new commit to the object store
4.  Changes the master branch (specifically, the ref refs/

    heads/master) to point to the new commit

In other words, Git adds the new commit to the end of the branch using the commit’s parent pointer, and advances the branch ref to the new commit.







Up until now, we've being thinking of a repository as a linear sequence of commits, like the one shown in Figure 3.

<figure><img src="../../.gitbook/assets/Group 36 (5).png" alt="" width="375"><figcaption></figcaption></figure>

Each commit points to the previous one, and main points to the last commit. Main is simply a pointer. Just a friendly name. Nothing special about main. Can be anything.&#x20;

We can create a new pointer to our commits, by invoking. don't worry about the commands for now.&#x20;

<figure><img src="../../.gitbook/assets/Group 37 (1).png" alt="" width="375"><figcaption></figcaption></figure>

What's the point of that, you might nbe wondring. Well, we can switch to the test pointer, do a new commit. In that case, test will move forward one position, pointing to the new commit, a22bc, but main will stay where it is, pointing at commit 53a3c.&#x20;

<figure><img src="../../.gitbook/assets/Group 38.png" alt="" width="375"><figcaption></figcaption></figure>



Now say we go back to main and do a commit:

<figure><img src="../../.gitbook/assets/Group 42.png" alt="" width="375"><figcaption></figcaption></figure>

Now our project has two separate lines of development: main and test. In Git terminology, main and test are _branches. A_ branch is simply a moveable pointer to a commit. Nothing more. Whenever you commit while on a branch, git automatically moves the branch pointer forward one commit.&#x20;

They are useful, since they allow&#x20;

## How Git keeps track of current branch

We've glossed over one important question: how does Git know which branch you're currently on? It keeps track via a special pointer called HEAD, which points to the branch we're currently on.&#x20;



<figure><img src="../../.gitbook/assets/Group 44.png" alt="" width="375"><figcaption></figcaption></figure>

When we're on main HEAD points to main, and if we when we're on test HEAD points to test. Swithing from one branch to another is done by changing where HEAD points to.&#x20;



Note that the HEAD pointer exists even if there's only one branch. Thus, a more accurate depiction of, for example, figure 1, would look like this:

<figure><img src="../../.gitbook/assets/Group 45.png" alt="" width="375"><figcaption></figcaption></figure>

## Reasons for using branches

Perhaps the easiest way to explain branches is via examples of common use use cases. Here are a few example:

## **Creating a branch**

Let's say you want to start working on a new feature. To keep those changes separate, you'd create a branch like this:

```
git branch new-feature 
```

This gives you a safe space to experiment without affecting your main codebase.

## **Switching to a branch**

To work on a specific branch, you'll need to switch to it. It's like changing lanes on a highway:

```
git checkout new-feature 
```

Now you're in the 'new-feature' lane, and any changes you make will only happen there.

## **Listing all branches**

Curious about what branches exist in your project? Use this command:

```
git branch
```

This will give you a list of your local branches. The one you're currently on will have a \* before it. &#x20;

## **Listing branch tree**

Want to get a visual understanding of how your branches connect? Try this:

```
git log --oneline --graph --decorate --all
```

This gives you a nice diagram of your branching structure, which can be super helpful for understanding your project's history.

## **Deleting branches**

Once you've finished with a branch (and you're sure it's merged into where it needs to be), you can delete it:

```
git branch -d old-branch
```

Just remember, you can't delete the branch you're currently standing on – you'll have to switch to a different one first.

* The index does not just contain changes to be made on the next commit; it is the next commit, a complete catalog of the files that will be included in the tree of the next commit (recall that each commit refers to a tree object that is a complete snapshot of the repository content). When you check out a branch, Git resets the index to match the tip commit of that branch; you then modify the index with commands such as git add/mv/rm to indicate changes to be part of the next commit.\

* “Deleting” a branch means simply deleting the correspond‐ ing ref; it has no immediate effect on the object store. In particular, deleting a branch does not delete any commits. What it may do, however, is make certain commits unin‐ teresting, in that they are no longer on any branch (that is, no longer reachable in the commit graph from any branch tip or tag). If this state persists, Git will eventually remove such commits from the object store as part of garbage col‐ lection. Until that happens, though, if you have an aban‐ doned commit’s ID you can still directly access it perfectly well by its SHA-1 name; the Git reflog (git log -g) is useful in this regard.

