# Commit Graph

The collection of all commits in a repository forms what in math‐ ematics is called a graph: visually, a set of objects with lines drawn between some pairs of them. In Git, the lines represent the com‐ mit parent relationship previously explained, and this structure is called the “commit graph” of the repository.

Because of the way Git works, there is some extra structure to this graph: the lines can be drawn with arrows pointing in one direc‐ tion because a commit refers to its parent, but not the other way around (we’ll see later the necessity and significance of this). Again using a mathematical term, this makes the graph “directed.” The commit graph might be a simple linear history, as shown in Figure 1-2.



Figure 1-2. A linear commit graph

Or a complex picture involving many branches and merges, as shown in Figure 1-3.



Figure 1-3. A more complex commit graph



Those are the next topics we’ll touch on.

What’s a DAG?

Git, by design, will not ever produce a graph that contains a loop; that is, a way to follow the arrows from one commit to another so that you arrive at the same commit twice (think what that could possibly mean in terms of a history of changes!). This is called being “acyclic”: not having a cycle, or loop. Thus the commit graph is technically a “directed acyclic graph,” or DAG for short.



































In a highly simplified view, we can think of a Git repository as a collection of commits. At their core, each commit represents a snapshot of the project at a specific point in time. Technically, the commit object itself doesn't store the content of the snapshot, but instead contains pointers to the snapshot. For simplicity, however, we won't get into the internals, and we'll think the commit as containing a snapshot of the project.&#x20;





A commit also consists of the following:

_Timestamp of commit_

Date and time the commit was made.

_Commit author's name and email_

&#x20;   \<explain how git gets this info>

_Commit message_

message entered when the commit is made. by looking at this you should have an understanding of what exactly the commit did to update the project.&#x20;

_A list of parent commits_

Usually one, but it can be zero or more. Root commit (typically one, but can be more). More than one parent indicates result of a merge. We'll discuss branches and merging later.

The set of all commits in a repository forms a directed acyclic graph (DAG).&#x20;



When a new commit is added, the branch pointer advances to the new commit.&#x20;

## How Git identifies commits

The simplest way we can imagine commits being named is by version numbers such as how other VCS's name commits. Git has a very different and unique approach. It uses a hash function. It takes as arguments the content of the commit and outputs a 160 bit string, representing by Git as a 40-hex digits.&#x20;

The unique thing about this approach is that the name of the commit is based on the content of it.&#x20;

if someone else has the same sha-1 for their commit, you can be sure you're both working on the same commit.

## Viewing commit history

The basic command to view the commit history is `git log`.&#x20;





By default, only prints commit's on the current branch--that is, commits reachable from the commit you're currently on. With multiple branches, you'd invoke:











## When to commit



When working on your own, it’s useful to commit “early and often,” so that you can explore different ideas and make changes freely without worrying about recovering earlier work. Such commits are likely to be somewhat disorganized and have cryptic commit messages, which is fine because they need to be intelligible only to you, and for a short period of time. Once a portion of your work is finished and you’re ready to share it with others, though, you may want to reorganize those commits, to make them well-factored with regard to reusability of the changes being made (especially with software), and to give them mean‐ ingful, well-written commit messages.
