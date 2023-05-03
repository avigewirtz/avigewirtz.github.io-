# Page 1

#### The Three States <a href="#_the_three_states" id="_the_three_states"></a>

Pay attention now — here is the main thing to remember about Git if you want the rest of your learning process to go smoothly. Git has three main states that your files can reside in: _modified_, _staged_, and _committed_:

* Modified means that you have changed the file but have not committed it to your database yet.
* Staged means that you have marked a modified file in its current version to go into your next commit snapshot.
* Committed means that the data is safely stored in your local database.

This leads us to the three main sections of a Git project: the working tree, the staging area, and the Git directory.

![Working tree, staging area, and Git directory](https://git-scm.com/book/en/v2/images/areas.png)Figure 6. Working tree, staging area, and Git directory

The working tree is a single checkout of one version of the project. These files are pulled out of the compressed database in the Git directory and placed on disk for you to use or modify.

The staging area is a file, generally contained in your Git directory, that stores information about what will go into your next commit. Its technical name in Git parlance is the “index”, but the phrase “staging area” works just as well.

The Git directory is where Git stores the metadata and object database for your project. This is the most important part of Git, and it is what is copied when you _clone_ a repository from another computer.

The basic Git workflow goes something like this:

1. You modify files in your working tree.
2. You selectively stage just those changes you want to be part of your next commit, which adds _only_those changes to the staging area.
3. You do a commit, which takes the files as they are in the staging area and stores that snapshot permanently to your Git directory.

If a particular version of a file is in the Git directory, it’s considered _committed_. If it has been modified and was added to the staging area, it is _staged_. And if it was changed since it was checked out but has not been staged, it is _modified_. In [Git Basics](https://git-scm.com/book/en/v2/ch00/ch02-git-basics-chapter), you’ll learn more about these states and how you can either take advantage of them or skip the staged part entirely.
