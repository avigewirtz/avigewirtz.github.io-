# Commits

## Commits

The core of a git repository is its committs. A commit is the only way to introduce a change into the repository. Each commit represents a snapshot of the project at a specific point in time.&#x20;

## Viewing commit history

* git log. prints every commit reachable from the commit you're currently on.
* will print following information for each commit:&#x20;
  * Commit ID - sha-1
  * Author of commit's name and email
  * timestamp of commit
  * Commit message

Git identifies each commit with a 40-hex-digit SHA-1 ID. Globally unqie. if someone else has the same sha-1 for their commit, you can be sure you're both working on the same project.&#x20;

### **When to Commit**

The timing for creating commits is up to you, but it's a good practice to commit whenever you've completed a logical chunk of work. For example, if you've implemented a new feature, tested it, and everything works, that's an ideal time to commit. Remember, it's usually better to have smaller, focused commits rather than massive ones that try to cram in many unrelated changes.

## How git history is represented

* Git history is DAG, Two properties: edges are directed, and no cycle
* regular commits have exactly one parent

Except for the first root commit, each commit is derived from one

The foundation of a git repository is the commits, so it makes sense to elaborate on it more.

Each commit has a pointer to its parent, besides for the first commit, which has no parent of course. The final commit also has a pointer to it, which is where the next commit will point to. By default, this pointer is called master. Consider a repository with three commits. If we commit again, the pointer moves forward automatically.&#x20;
