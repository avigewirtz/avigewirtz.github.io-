# Local Git workflow

There are&#x20;



We'll explain the basics of git using entirely one repository.&#x20;

First, let's create a project directory, which we'll call git\_practice:

```
mkdir git_practice
cd git_practice
```





Assume local environment personal project you want to track.



Assume we have directory that looks like this.

You have a project you want to track.&#x20;



1. Create a repository.
2. Save a snapshot of your project to the repository.&#x20;
3. Edit your project.&#x20;
4. Save the new snapshot to your repository.&#x20;
5. Repeat steps 3-4 as necessary.&#x20;

Let's go over these steps one by one. We'll go over reverting to a previous snapshot later.&#x20;

## Creating a repository

Within the project directory, you create what is known as a repository by invoking `git init.` (init is short for initialize). This creates a subdirectory named .git, where the git repository is stored. A Git repository is essentially a database that holds all the necessary information for maintaining and managing a project's files and history.&#x20;

Since we just created the repository, it will be empty.&#x20;

## Saving files

An important thing to recognize that Git does not automatically save anything in our repository.  changes. In other words, it's not like an autosave, where every time you type your work is saved. We have to manually save our work. Our goal is to save the three files in our directory.

Saving work is a two step process, involving staging and committing. First, you have to tell git which files you want it to include in the saved snapshot of your directory. This is called staging. This may seem redundant, since you likely want to save all files. In this step, you selectively choose the changes you want to include in the next commit.

To stage, invoke git add followed by the names of the files you want to stage. In our case:

```
git add intmath.c testintmath.c
```

If you want to stage all relevant files, you can save time by using the `*` [wildcard](../the-linux-command-line/useful-command-line-features.md#wildcards):

```bash
git add * 
```

To actually save the files, you invoke the git commit command. All files in the stagin area will be included in the commit. Git requires you to add a commit message with each commit. For first commit not much to say, but for later commits important.&#x20;

```bash
git commit -m "first commit" 
```

note that the quotation marks are part of the command.&#x20;



**Editing and Saving More Snapshots**

Now, let's assume we make a couple of changes to our project. For example, we modify testintmath.c, and we create a new file named circle.c. To save a new snapshot that reflects these changes, we invoke:

```
git add intmath.c circle.c
git commit -m "fixed bug in testintmath.c. added circle.c"
```

Notice that this time with git add, we need only list intmath.c. and circle.c. Any other file that was previously commited but hasn't changed is automatically a part of the new snapshot.&#x20;

















\








