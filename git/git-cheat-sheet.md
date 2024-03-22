# Git Cheatsheet

### Basic Git Commands

* `git init` Initialize a new Git repository.
* `git clone <repository>`: Clone an existing repository.
* `git status`: Check the status of your working directory.
* `git add <file>`: Add a file or changes to the staging area.
* `git add .`: Add all changes in the working directory to the staging area.
* `git commit -m "Your commit message"`: Commit your changes with a message.
* `git log`: View the commit history.

### Remote Repositories

* `git remote`: List remote repositories connected to your local repository.
* `git remote add <name> <url>`: Add a remote repository.
* `git remote remove <name>`: Remove a remote repository.
* `git fetch <remote-name>`: Fetch changes from a remote repository.
* `git pull <remote-name> <branch-name>`: Fetch and merge changes from a remote branch.
* `git push <remote-name> <branch-name>`: Push your local branch to the remote repository.
* `git push --set-upstream <remote-name> <branch-name>`: Set the upstream branch for the current branch.
