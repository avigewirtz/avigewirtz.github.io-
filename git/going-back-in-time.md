# Going back in time

At any stage, you may want to view a previous commit, or you might want to reset to that stage.&#x20;

For example, suppose we have a project with 4 commits. we either want to view commit number 2, or reset to it.&#x20;





## How  commits are stored



Before we can discuss how to go back to previous commit, we need to have a basic understanding of how commits&#x20;

In order to explain this, we first have the represented internally.

<figure><img src="../.gitbook/assets/Group 20 (6).png" alt="" width="375"><figcaption></figcaption></figure>





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
git reset <hash>
```

This moves both HEAD and main. main now points to commit 2, and HEAD points to main.&#x20;



## Doing a reset with "non-clean" working directory

In the previous examples, we assumed that the working directory was "clean." Meaning \<fill in>. What happens if...



go over case for git checkout



go over deault case for git reset

go over git reset --soft and --hard options











