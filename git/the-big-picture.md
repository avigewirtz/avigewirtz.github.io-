# The big picture

How version control works with git



The basic idea of how version control is done in git is that the project under version control has a .git directory in the root of the project's workspace which contains a git repository. A git repository is essentially a database that keeps track of all your project's changes.&#x20;

&#x20;

## Commits not autosave



An important thing to recognize&#x20;



## Obtaining a Git repository

There are two ways to obtain a git repository. The first is to create a new one for a project that's currently not under version control. The second is to copy, or clone in git teminology, an existing repository.&#x20;





## Collaboration with git

In addition to basic local version control, git can also be used to enable developers to collaborate with each other. The basic idea of collboration is for two repositories to be able to exchnage data between each other. For example, it might be two students collaborating on an assignment. In the context of a data exhange, the repository you're working in is called the local repository, while the other is called a remote repository. Note that a remote repository may be loicated on the same computer.&#x20;



It is possible for any two repositories to exhcnage data directy. For example, for two students to exchnage.&#x20;



This is bad practice, however. See here for a detailed explanation on why.



The reccomended workflow is to have a central repository that neither you nor anyone works in. In other words, that has no worktree. Such a repository is called a bare repository. The point of this repository is to be used for syncing up.&#x20;



Furthermore, it's typically a good idea to host the central repository on a server that is easily accessible by everyone. One such example is github.&#x20;



