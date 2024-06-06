# Commits Graph


- in components of git project I'll go over commits 

We know that eachh commit represents a snapshot of project at certain point in time.&#x20;

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

The complete history of all commits in a repository forms a “commit graph”. You can print rhe commit graph using the git log command. assuming you've followed along in the previous section, you're commit graph will look like the following: 

To display the commit graph of your project, you can invoke git log with the `--graph` and `--all` options:

```bash
git log --all --graph
```


A visual representation of this graph is shown in Fugure 20. 

<figure><img src="../../.gitbook/assets/Group 410.png" alt="" width="375"><figcaption><p>Figure 1-2: A linear commit graph</p></figcaption></figure>

Figure 1-2. A linear commit graph


Each node represents a commit, labeled by the first 5 letters of the commit's sha-1 hash (see below).  


Arrows point from a commit to its parents. The first commit has no parents is called the “root commit”. 

the latest commit is pointed to by main, which in turn is pointed to by HEAD. 



The labels on the right side of this picture—master, topic, and release—denote “branches.” The branch name refers to the latest commit on that branch; here, commits F, 4, and Z, respectively, are called the “tip” of the branch. The branch itself is defined as the collection of all commits in the graph that are reachable from the tip by following the parent arrows backward along the history. Here, the branches are:


{% hint style="info" %}
A commit graph has two characteristics: it is _directed_, meaning that the nodes can only be traversed in one direction, and _acyclic_, meaning the graph does not contain any loops (i.e., a way to follow traverse the graph and encounter the same commit twice). In mathematical terms, this is called a _directed acyclic graph,_ or DAG for short.&#x20;
{% endhint %}

