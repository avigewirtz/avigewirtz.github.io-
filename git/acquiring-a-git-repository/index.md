# Index

Index can be source of confusion, son worthwhile to dedicate a section to it.&#x20;



The Git “index” often seems a bit mysterious to people: some invisible, ineffable place where changes are “staged” until they’re committed. The talk about “staging changes” in the index also suggests that it holds only changes, as if it were a collection of diffs waiting to be applied.



The truth is different and quite simple, and critical to grasp in order to understand Git well. The index is an independent data structure, separate from both your work‐ ing tree and from any commit. It is simply a list of file pathnames together with associated attributes, usually including the ID of a blob in the object database holding the data for a version of that file. You can see the current contents of the index with git ls- files:



If you were to delete or change any of the listed files in your working tree, this would not affect the output of this command at all; it’s not looking at them.





A few key points to understand about the index:

* Contains unmodified files as well. Not only changes. The index does not just contain changes to be made on the next commit; it is the next commit, a complete catalog of. the files that will be included in the tree of the next commit (recall that each commit refers to a tree object that is a complete snapshot of the repository content). When you check out a branch, Git resets the index to match the tip commit of that branch; you then modify the index with commands such as git add/mv/rm to indicate changes to be part of the next commit.
* git add does not just note in the index that a file has changed; it actually adds the current file content to the ob‐ ject database as a new blob, and updates the index entry for that file to refer to that blob. This is why git commit is always fast, even if you’re making lots of changes: all the actual data has already been stored by preceding git add commands.
* An implication of this behavior that occasionally confuses people is that if you change a file, git add it, then change it again, it is the version you last added to the index, not the one in your working tree, that is part of the next commit. git status shows this explicitly, by listing the same file as having both “changes to be committed” and “changes not staged for commit.”
* When you add to index, it saves a snapshot of that file
* not a list of files. includes content
