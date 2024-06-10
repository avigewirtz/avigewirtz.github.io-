# Commits

Now that we've made a few commits, let's take a closer look at&#x20;





&#x20;how Git tracks changes using the commit graph.&#x20;

Things we'll cover:

* What exactly is contained in each commit
* How git identifies commits
* How git stores history of commits



Git stores the history of commits in a structure known as a directed acyclic graph (DAG).&#x20;

The complete history of all commits in a repository forms a “commit graph”. Each node in this graph is a commit, which contains information about the changes made, the author, the commit message, and a reference to its parent commit(s). In our case, with a single branch and linear history, this graph forms a simple, straight line.

Directed, meaning you can only traverse in one direction, and acyclic, meaning you'll never encounter the same node twice in a traversal.&#x20;

<figure><img src="../.gitbook/assets/Group 410.png" alt="" width="375"><figcaption><p>Figure 1-2: A linear commit graph</p></figcaption></figure>

Figure 1-2. A linear commit graph

Each node represents a commit, labeled by the first 5 letters of the commit's sha-1 hash (see below).

Arrows point from a commit to its parents. The first commit has no parents is called the “root commit”.

the latest commit is pointed to by main, which in turn is pointed to by HEAD.



{% hint style="info" %}
A commit graph has two characteristics: it is _directed_, meaning that the nodes can only be traversed in one direction, and _acyclic_, meaning the graph does not contain any loops (i.e., a way to follow traverse the graph and encounter the same commit twice). In mathematical terms, this is called a _directed acyclic graph,_ or DAG for short.
{% endhint %}



## How Git identifies commits



A pointer to its parent commits. As we'll soon see, most commit have a single parent, but they can have no parents (such a commit is called a root commit) or multiple parents (this is called a merge commit). Most commits have a single parent, indicating that they evolved in a straightforward way from a single previous state of the project. This is called a “root commit,” and most often, there is only one root commit in a repository—the initial one created when the repository was started. However, you can introduce multiple root commits if you want; the command git checkout --orphan does this. When a commit has more than one parent, this indicates a “merge,” in which the committer has incorporated the changes from multiple lines of development into a single commit.





The simplest way we can imagine commits being named is by version numbers such as how other VCS's name commits. Git has a very different and unique approach. It uses a hash function. It takes as arguments the content of the commit and outputs a 160 bit string, representing by Git as a 40-hex digits.

The unique thing about this approach is that the name of the commit is based on the content of it.

if someone else has the same sha-1 for their commit, you can be sure you're both working on the same commit.
