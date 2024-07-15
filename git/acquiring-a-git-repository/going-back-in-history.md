# Going Back in History

Three things you might want to do:

1. View an old commit
2. Go back to a previous commit while deleting history
3. go back but maintain history

In this section, we'll go over how to do all three.&#x20;

To understand how this works, we need to take a step back and examine how Git stores the commit history.&#x20;

#### Commit Graph

Our repository currently has 6 commits. We mentioned earlier that each commit contains a reference to its parent commit (besides for the root commit, which has no parents). The entire history of commits forms a commit graph, which visually looks like the following:

A <- B <- C <- D <- E <- F

In this representation, ‘A’ is the root commit with no parents, and each subsequent commit (B, C, D, E, F) points to its immediate predecessor.

This graph can only be traversed in the direction of the arrows. Meaning, all nodes are reachable from F, but only A and B are reachable from C.

How does Git know which commit we’re currently on? Simple. It stores its hash in a moveable pointer called HEAD. By default, the commit we’re on will be the most recent commit:

A <- B <- C <- D <- E <- F <- HEAD

In fact, this is an oversimplification. HEAD points to another moveable pointer, main, which points to F:

Each time we commit, main automatically moves to the next commit. So, for example, if we were to make a new commit, G, our graph would now look like this:

A <- B <- C <- D <- E <- F <- G <- HEAD

Until we cover reverting history and branching, the reason for two pointers won’t make much sense. For the time being, just note that this is the case.



#### Examining an earlier state of your project

To examine an earlier state of your project, you can use the `git checkout <commit-hash>` command. This command allows you to switch your working directory to the state of a specific commit, identified by its unique commit hash. This way, you can explore the project's files and code as they were at that point in time. However, it's important to note that using `git checkout` in this manner will put you in a "detached HEAD" state, meaning you're not on any branch. This is useful for examining past states, but any changes you make won't be tied to a branch unless you create a new branch from this state.



#### Resetting to an earlier state

Resetting to an earlier state is achieved using the `git reset` command. This command comes with different options that determine the extent of the reset. `git reset --hard <commit-hash>` is the most aggressive option, moving the branch pointer to the specified commit and discarding all changes made after that commit in both the working directory and the staging area. This effectively reverts the project to the exact state of the specified commit, but it is destructive and can lead to loss of work if not used carefully. Alternatively, `git reset --soft <commit-hash>` resets the branch to the specified commit but leaves all changes made after that commit staged in the index, allowing you to recommit them if needed.

#### Going back to an earlier state without losing history

Going back to an earlier state without losing history is done using the `git revert <commit-hash>` command. This command creates a new commit that undoes the changes introduced by the specified commit, without altering the existing commit history. It is a safer and more transparent method, as it maintains a clear record of all changes, including the reversion. This approach is ideal when you need to undo specific changes but still want to preserve the project's history for future reference and collaboration.

## How  commits are stored



Before we can discuss how to go back to previous commit, we need to have a basic understanding of how commits&#x20;

In order to explain this, we first have the represented internally.

<figure><img src="../../.gitbook/assets/Group 20 (6) (1).png" alt="" width="375"><figcaption></figcaption></figure>





You might be wondering why there's two pointers. seems redundant. Hold onto that thought for now. It should make a bit more sense shortly, but it'll especially make sense when we diascuss branching.&#x20;

## Examining a previous commit

Suppose we want to examine commit 2, but we don't want to reset to it. To temporarily go back to a previous commit, we can use `git checkout` followed by the commit 2s hash. Reacll that we can find out the commit hash by invoking git log:



To go back to commit 2, we invoke:

```
git checkout <hash>
```

What this does it it sets the HEAD pointer to now point to commit two, but leaves the main pointer in place.

It is imperative that when you finish viewing the commit, you point the head back to main.&#x20;

## Reseting to a previous commit



```
git reset -
```

This moves both HEAD and main. main now points to commit 2, and HEAD points to main.&#x20;



## Doing a reset with "non-clean" working directory

In the previous examples, we assumed that the working directory was "clean." Meaning \<fill in>. What happens if...



go over case for git checkout



go over deault case for git reset

go over git reset --soft and --hard options











