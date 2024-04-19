# Understanding the index

Before we discuss how to record changes to a repository, critical to grasp how the index works. Once you understand this, recording changes will be much easier.&#x20;

1. index is often thought of as a place where changes are stored, but in fact the entire next snapshot is stored there.&#x20;

<figure><img src="../../.gitbook/assets/Group 141 (4).png" alt=""><figcaption></figcaption></figure>

## Modifying working tree and recording changes

## Index

Before we discuss how to record changes to a repository, critical to grasp how the index works. Once you understand this, recording changes will be much easier.&#x20;

1. Index matches checked out commit. index is often thought of as a place where changes are stored, but in fact the entire next snapshot is stored there. If that is the case, why do we only add changes to the index, but not unmodified files? Unmodified files from last commit remain in the index. It's not like the index gets wiped clean after a commit. We can verify this by viewing the contents of the index immediatey after out last commit, which can be done with git ls-files. We can view the contents of the index by invoking git ls-file. If we do that now, we see that bye/bye.txt, hello.txt, and hi.txt, which are unmodified, are still listed in the index, even though we didn't "add" them since the last commit. In other words, it's true that you only have to stage modified or untracked files, but that's because unmodified files are automatically staged.
2. not just a list of pathnames. contains actual content of file in state it was in at time it was staged. When you add a file to the index, git creates a copy of the file in a binary format, known as a blob, which the index entry points to. The index does not point to the version in the working tree. it points to the blob.&#x20;
3. Explains a few things:
   1. When you delete a file in working directory and invoke git ls-file, you'll see that it's still there. That's because the index still references the copy of the file, which is independent of the file in the working directory. This explains why when you delete a file in the working directory, you have to let the index know about this change.&#x20;

## Index



* what actually happens when you add a file to the index:

The Git “index” often seems a bit mysterious to people: some invisible, ineffable place where changes are “staged” until they’re committed. What exactly does it mean to add content to the index? are we simply adding the filename? and does the index only contain changes, or the entire snapshot to be committed?

* not just a list of files. contains actual content of file. In other words, when you add a file to the index, git does more than simply record it's name. git creates an object for the file, known as "blob", which the index points to.&#x20;

{% hint style="warning" %}
**Note**: Technically, the index does not store the actual content of the files directly. Instead, it stores references (or pointers) to the content, which are kept in what Git calls "blobs." These blobs are stored in the object database of Git, and the index keeps track of these references along with metadata about the staging state of each file.
{% endhint %}



The Git “index” often seems a bit mysterious to people: some invisible, ineffable place where changes are “staged” until they’re committed. The talk about “staging changes” in the index also suggests that it holds only changes, as if it were a collection of diffs waiting to be applied.



The truth is different and quite simple, and critical to grasp in order to understand Git well. The index is an independent data structure, separate from both your work‐ ing tree and from any commit. It is simply a list of file pathnames together with associated attributes, usually including the ID of a blob in the object database holding the data for a version of that file.&#x20;





You can see the current contents of the index with git ls- files:



We see that after a commit, all three files are in the index.&#x20;



this helps explain a few things:

* if you delete a file in the working tree, has no effect on the index.
* If you modify a file in the working tree, has no effect on th eindex

If you were to delete or change any of the listed files in your working tree, this would not affect the output of this command at all; it’s not looking at them.





