# Commits

The foundation of a git repository is the commits, so it makes sense to elaborate on it more.



Each commit has a pointer to its parent, besides for the first commit, which has no parent of course. The final commit also has a pointer to it, which is where the next commit will point to. By default, this pointer is called master. Consider a repository with three commits. If we commit again, the pointer moves forward automatically.&#x20;
