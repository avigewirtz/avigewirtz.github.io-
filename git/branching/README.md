# Branching

Branching means you diverge from the main line of development and continue to do work without messing with that main line.





Up until now, we've being thinking of a repository as a linear sequence of commits. Each commit has a pointer to its parent, besides for the first commit, which has no parent of course. The final commit also has a pointer to it, which is where the next commit will point to. By default, this pointer is called master. Consider a repository with three commits.&#x20;



If we commit again, the pointer moves forward automatically.&#x20;



In addition to the master, git has another pointer, called HEAD, which points to master. This may seem pointless, but we'll shortly see the reasoning behind this.&#x20;



We can create a new pointer to one of the commits. We'll show the command for doing so shortly. For now, let's assume we create another pointer, which we'll call B. By default, B will point to the same commit we're currently on:&#x20;

Now master, which is pointed to by HEAD, moves forward to the latest commit, but B still points to the latest commit.&#x20;





At this point you're probably wondering, what's the point of all of this? Well, suppose we now change HEAD to point to B, rather than master. We'll show the command for doing this later. Here's the updated figure:





If we now commit, B, which is pointed to by HEAD, will move forward one position, but in a seperate&#x20;



`it creates a new commit, which is completely different than the commit than B points to. Now, our project has diverged into two seperate paths.`&#x20;



master and B are branches. A branch is simply a pointer to a commit. "working" on a branch simply means the HEAD points to it.&#x20;



### Creating a branch







### Switching to a branch







### Viewing branches



### Viewing branch tree





