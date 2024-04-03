# Branching

Up until now, we've being thinking of a repository as a linear sequence of commits, like the one shown in Figure 3.

<figure><img src="../../.gitbook/assets/Group 36 (5).png" alt="" width="375"><figcaption></figcaption></figure>

Each commit points to the previous one, and main points to the last commit. Main is simply a pointer. Just a friendly name. Nothing special about main. Can be anything.&#x20;

We can create a new pointer to our commits, by invoking. don't worry about the commands for now.&#x20;

<figure><img src="../../.gitbook/assets/Group 37 (1).png" alt="" width="375"><figcaption></figcaption></figure>

What's the point of that, you might nbe wondring. Well, we can switch to the test pointer, do a new commit. In that case, test will move forward one position, pointing to the new commit, a22bc, but main will stay where it is, pointing at commit 53a3c.&#x20;

<figure><img src="../../.gitbook/assets/Group 38.png" alt="" width="375"><figcaption></figcaption></figure>



Now say we go back to main and do a commit:

<figure><img src="../../.gitbook/assets/Group 42.png" alt="" width="375"><figcaption></figcaption></figure>

Now our project has two separate lines of development: main and test. In Git terminology, main and test are _branches. A_ branch is simply a pointer to a commit. Nothing more. They are useful, since they allow&#x20;

## HEAD

We've glossed over one important question: how does Git know which branch we're currently on? It keeps track via a special pointer called HEAD, which points to the branch we're currently on.&#x20;



<figure><img src="../../.gitbook/assets/Group 44.png" alt="" width="375"><figcaption></figcaption></figure>

When we're on main HEAD points to main, and if we when we're on test HEAD points to test. Swithing from one branch to another is done by changing where HEAD points to.&#x20;



Note that the HEAD pointer exists even if there's only one branch. Thus, a more accurate depiction of, for example, figure 1, would look like this:

<figure><img src="../../.gitbook/assets/Group 45.png" alt="" width="375"><figcaption></figcaption></figure>

## Creating a branch

Now that we've given a conceptual overview of branching, let's dig into the commands.&#x20;

## Switching to a branch



### Listing all branches



### Listing branch tree









