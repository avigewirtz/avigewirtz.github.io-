# Commits

## What's in a commit

At its core, a commit represents a snapshot of the entire project at a specific point in time. Additionally, a commit also contains along metadata that provides context about the snapshot. Specifically, it contains:

* The commit author's name and email.&#x20;
* The time and date the commit was made
* The commit message. The message git requires you to provide when making a commit. It should be descriptive, explaining the purpose of the changes.
* A pointer to its parent commits. As we'll soon see, most commit have a single parent, but they can have no parents (such a commit is called a root commit) or multiple parents (this is called a merge commit).  Most commits have a single parent, indicating that they evolved in a straightforward way from a single previous state of the project. This is called a “root commit,” and most often, there is only one root commit in a repository—the initial one created when the repository was started. However, you can introduce multiple root commits if you want; the command git checkout --orphan does this. When a commit has more than one parent, this indicates a “merge,” in which the committer has incorporated the changes from multiple lines of development into a single commit.&#x20;



{% hint style="warning" %}
&#x20;Technically, the commit itself doesn't store the content of the snapshot, but instead contains pointers to the snapshot. For simplicity, however, we won't get into the internals, and we'll think the commit as containing a snapshot of the project.&#x20;
{% endhint %}

## How Git identifies commits

The simplest way we can imagine commits being named is by version numbers such as how other VCS's name commits. Git has a very different and unique approach. It uses a hash function. It takes as arguments the content of the commit and outputs a 160 bit string, representing by Git as a 40-hex digits.&#x20;

The unique thing about this approach is that the name of the commit is based on the content of it.&#x20;

if someone else has the same sha-1 for their commit, you can be sure you're both working on the same commit.

## Commit graph

The set of all commits in a repository forms a “commit graph”. The commit graph might be a simple linear history, as shown in Figure 1-2.

<figure><img src="../../.gitbook/assets/Group 410.png" alt="" width="375"><figcaption><p>Figure 1-2: A linear commit graph</p></figcaption></figure>

Figure 1-2. A linear commit graph

Or a complex graph involving several branches and merges, as shown in Figure 1-3.

<figure><img src="../../.gitbook/assets/Group 426 (1).png" alt=""><figcaption></figcaption></figure>

Each node represents a commit, labeled by the first 5 letters of the commit's sha-1 hash.  Arrows point from a commit to its parents. Commit 3b917 has no parents and is called a “root commit”; it was the initial commit in this repository’s history. Most commits have a single parent, indicating that they evolved in a straightforward way from a single previous state of the project. Some commits, here just commit 9c527, have multiple parents and are called “merge commits.” This indicates that the commit is derived by merging distinct branches of the commit graph. We’ll define branches and merges more precisely in a moment.



The labels on the right side of this picture—master, topic, and release—denote “branches.” The branch name refers to the latest commit on that branch; here, commits F, 4, and Z, respectively, are called the “tip” of the branch. The branch itself is defined as the collection of all commits in the graph that are reachable from the tip by following the parent arrows backward along the history. Here, the branches are:

* release = {A, B, C, X, Y, Z}
* master = {A, B, C, D, E, F, 1, 2}

Overview | 3

• topic = {A, B, 1, 2, 3, 4}

{% hint style="info" %}
A commit graph has two characteristics: it is _directed_, meaning that the nodes can only be traversed in one direction, and _acyclic_, meaning the graph does not contain any loops (i.e., a way to follow traverse the graph and encounter the same commit twice). In mathematical terms, this is called a _directed acyclic graph,_ or DAG for short.&#x20;
{% endhint %}

## Viewing the commit graph

To display the commit graph of your project, you can invoke git log with the `--graph` and `--all` options:

```bash
git log --all --graph
```

This shows a graphical representation of the entire commit history of your project, starting with the most recent commit. The entry for each commit includes its 40-digit SHA-1 hash, the author's information (name and email), the timestamp, and the commit message.
