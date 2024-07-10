# Components of a Git Project

#### Components of a Git Project

Before we delve into the details of recording changes to a repository, let's ensure we understand the components of a Git project. As our example has hopefully shown, a Git project consists of three main components:

* The working tree. A working copy of a specific commit, plus any changes.
* The index, or staging area. Contains the files that will be the next commit. Essentially a pseudocommit. A few important, often misunderstood points about the index:
  * Not just changes, but entire next commit. As we'll see below, we only need to explicitly add new or modified files, since unmodified files are automatically in index.&#x20;
  * When you add files to the index, git does more than just record the filenames in the index. It creates a copy of the files at the time you added it to the index. Index contains pointer to copy of each file. For simplicity, we'll avoid getting into git internals and assume actual contents are stored in index. The important thing to understand is that adding a file to the index creates a copy, which is what the index looks at. It does not look at the version of the file in your working tree.&#x20;
  *   An important thing to recognize is that after a commit, the index isn't wiped clean. All the files we just committed remain in the index. You can verify this by running git ls-files:

      ```bash
      git ls-files
      ```

      For this reason, in subsequent we only need to add new or modified files. We don't need to add unmodified files, since they're already in the index from the previous commit.&#x20;
* The commit history. The actual snapshots of the project at various points in the time. This is the core of the repository. Again, the commit itself does not store the contents of the snapshot, but a pointer to the contents. For simplicity, however, we'll assume contents of snapshot are stored in commit.  Additionally, a commit also contains the following metadata that provides context about the commit:&#x20;
  * The commit author's name and email.
  * The time and date the commit was made.
  * The commit message.&#x20;
  * A pointer to its parent commit(s).
