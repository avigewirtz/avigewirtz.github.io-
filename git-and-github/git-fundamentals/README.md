# Git Fundamentals

Before issuing Git commands, it's important to have a high-level overview of how Git works. &#x20;

## Git repositories

A Git repository is essentially a database that holds all the necessary information for maintaining and managing a project's files and history. The repository is typically stored at the root of the project’s workspace in a hidden directory named _.git_.

The .git directory contains numerous files and subdirectories, each holding vital information needed to version control the project. Some key components stored in the _.git_ directory include:

* A copy of all project files under Git version control.
* Records of all changes made to the files at various stages of development. These records include information such as the author of the change and the timestamp of the change.&#x20;
* References to other repositories that the repository may want to interact with. This topic will be further discussed in the section on remotes.

&#x20;
