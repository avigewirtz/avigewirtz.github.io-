# Staging Files

git add is a command that allows you to stage changes in your working directory, preparing them to be committed to the repository. Staging changes means that you're telling Git you want to include those specific changes in the next commit. This is useful for organizing your work into logical units or separating unrelated changes.

For the repository https://github.com/COS217/Decomment as a reference, you might want to stage files in the following scenarios:

\


1\. Adding a file. Suppose you've created a new file named decomment.c that contains the main implementation of the Decomment project. After creating the file, you would stage it using git add:

\


| git add decomment.c |
| ------------------- |

\


2\. Modifying a file. Suppose you've made changes to decomment.c, such as adding a new function or improving existing code. After making the changes, you would stage the modified file again:

\


| git add decomment.c |
| ------------------- |

\


Similarly, suppose you've populated the readme file, as required at the end of the assignment. If you want to include the populated readme file in your Git repository, you would stage the updated file:

\


| git add readme |
| -------------- |

\
\


Common usage:

1. Staging a single file:

| git add file |
| ------------ |

\


2. Staging multiple files:

| git add file1 file2 file3 |
| ------------------------- |

\


3. Staging all changes in the working directory:

| git add . |
| --------- |

The . refers to the current working directory, so this command will stage all modified and new files (but not deleted files).
