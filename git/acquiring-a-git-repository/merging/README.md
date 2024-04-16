# Merging

important to understand that merging inherently flawed process.



* merging one branch into another.&#x20;

Over here, will only go over merging two branches

## Types of merges

* Fast forward merge
* 3-way merge. 3-way merge is inherently flawed procedure.&#x20;



## Merging in a nutshell

## Fast forward merge

on main branch, and test brach is two commits ahead, but branches have no diverged.&#x20;

<figure><img src="../../../.gitbook/assets/Group 234 (1).png" alt="" width="375"><figcaption></figcaption></figure>







result after merge:

<figure><img src="../../../.gitbook/assets/Group 235.png" alt="" width="375"><figcaption></figcaption></figure>



h

## 3-way merge

<figure><img src="../../../.gitbook/assets/Group 236.png" alt="" width="375"><figcaption></figcaption></figure>



<figure><img src="../../../.gitbook/assets/Group 242 (1) (1).png" alt="" width="563"><figcaption></figcaption></figure>

merges one branch into another. Merges commits. For example, say we have two branches: main and test. We're currently on main, which points to C8, and we went to merge test, which points to C9, with main.

The basic idea is git merges contents of C8 and C9, creating a new commit, C10, for the result.  To do so, we'd invoke:

```
git merge test
```

main will be moved forward to point to C10, but test will remain where it is, pointing at C9. C10 has two parents, hence all commits are reachable from it.&#x20;

After a merge, we'll typically delete the branch we merged from, since it's no longer needed. In our case, we might delete test.&#x20;

There are a few important things to understand about merges:

* 3-way merge
* in certain cases, merge won't succeed. Requires human intervention
* inherently flawed process. even if it succeeds, does not mean resuting code is correct.&#x20;

