# How Git Identifies Commits

In some older version control systems, commits were identified by sequential numbers or dotted strings that reflect the order in which they were made. For example, in CVS, a commit might be identified by a number like 2.17.1.3. This number is a counter that increments with each new commit, and its primary purpose is to indicate the sequence of changes.

Git uses a different approach for identifying commits. Instead of sequential numbers, Git uses content-based addressing, which means that the identifier for a commit is derived from the commit's content. This is achieved through a process called hashing, specifically using the SHA-1 hash function.

When you create a commit in Git, it generates a SHA-1 hash based on the commit's content. This content includes several pieces of information:

* The commit message.
* The author's name and email.
* The timestamp of the commit.
* A reference to the parent commit(s).
* A reference to the tree object that represents the state of the files at the time of the commit.

The SHA-1 hash function takes all this information and produces a unique 160-bit string, which is represented as a 40-character hexadecimal number. A SHA-1 hash might look like this:

```
f4c3b4d5e6f7a1b2c3d4e5f6a7b8c9d0e1f2a3b4
```

Because Git uses the commit's actual content to generate the identifier, the same content will always produce the same SHA-1 hash. This ensures that each commit is uniquely identified by its content, and even a small change in the commit (such as a different commit message or a different timestamp) will result in a completely different hash.
