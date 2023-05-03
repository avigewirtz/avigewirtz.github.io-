# Acquiring a Git Repository

There are two ways you can acquire a Git repository:&#x20;

1. You can create a new Git repository.&#x20;
2. You can copy an existing Git repository.

## Creating a Git Repository

Creating a repository means initializing a repository in a directory that is not currently under Git version control. The process is extremely simple. You simply navigate to the directory you want to version control and invoke `git init`. For example, to create a Git repository in git\_practice, perform these steps:

```bash
# navigate to git_practice
cd ~/git_practice
# create a git repository
git init 
```

_git\_practice_ will now contain a _.git_ subdirectory, which contains your Git repository. You can confirm this by invoking _ls -a_.

An important thing to recognize with Git is that Git does not automatically save any content from your working directory. Therefore, the newly created Git repository is a mere skeleton repository--that is, it does not contain the contents of git\_practice.&#x20;

You must manually tell Git to save the contents. Similarly, if after Git saved a file you modified the file, Git will not contain the updated version. You must tell Git at each point in time that you'd like it to record the contents of the file.&#x20;

## Staging Files

Saving files essentially involves telling git to save a snapshot of your current project. However, saving is a two-step process. Before you can save files to your repository, you must first add them to an intermediate area called the index or staging area. This process is called "staging." In this step, you must specify which files you want to stage. For example, in git\_practice, i can stage just one file--such as hello.c--two files, or all three.&#x20;



## Committing Files

To finalize the saving process I need to commit the files in the staging area. However, when I commit I don't specify which files to commit. I simply tell git I want to commit, and it commits all files in the staging area. That is the purpose of the staging area--to selectively choose which files I want to be included.&#x20;



## Practice

We will practice basic Git commands using a directory named git\_practice containing 3 files: hello.c, circle1.c, and circle2.c.&#x20;

To obtain the git\_practice directory, you can simply paste the following code block on the command line.

```bash
git clone https://github.com/avigewirtz/git_practice.git && cd git_practice && rm -rf .git
```

Your working directory will now be git\_practice.

First, invoke `ls -a`, and notice that there is no .git subdirectory:



<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 3.56.14 PM.png" alt=""><figcaption></figcaption></figure>

You can also invoke git status--an important command we will elaborate on soon--and you should get the following output: fatal: `not a git repository (or any of the parent directories): .git`. To create a Git repository, simply invoke git init:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 3.57.17 PM.png" alt=""><figcaption></figcaption></figure>

Now invoke ls -a again, and notice that the repository contains a .git subdirectory:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 3.59.00 PM.png" alt=""><figcaption></figcaption></figure>

We will now perform a few steps to give you the hang of how Git works:

1. git status

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 4.00.05 PM (1).png" alt=""><figcaption></figcaption></figure>



git add

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 4.00.59 PM.png" alt=""><figcaption></figcaption></figure>

git status

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 4.01.22 PM.png" alt=""><figcaption></figcaption></figure>

git commit

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 4.01.47 PM.png" alt=""><figcaption></figcaption></figure>



Adding a new file:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 4.02.30 PM.png" alt=""><figcaption></figcaption></figure>

git status

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 4.03.19 PM.png" alt=""><figcaption></figcaption></figure>

git add using \* wildcard

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 4.04.08 PM.png" alt=""><figcaption></figcaption></figure>



<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 4.04.58 PM.png" alt=""><figcaption></figcaption></figure>







<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 4.05.19 PM.png" alt=""><figcaption></figcaption></figure>



<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 4.06.35 PM.png" alt=""><figcaption></figcaption></figure>



<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 4.06.55 PM.png" alt=""><figcaption></figcaption></figure>



<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 4.08.23 PM.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 4.09.32 PM.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 4.09.48 PM.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 4.10.46 PM.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 4.11.02 PM.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-03 at 3.56.14 PM (1).png" alt=""><figcaption></figcaption></figure>



```
git add hello.c circle1.c circle2.c\
```

```bash
# alternatively, you can use the "*" wildcard:
git add *
```

Once you have added the files to the staging area, you can commit them:

```bash
git commit 
```

Git will not open your text editor and prompt you for a commit message. A commit message is simply a means of documenting the changes you made. It can be anything from a simple "first commit" to an "updated xyz bug."&#x20;

Alternatively, you can provide the commit message with the `git commit` command using the `-m` option:

```bash
git commit -m "descriptive message"
```

when you commit, you don't specify files. All the files in the staging area will be included in the commit. You don't have to worry about commiting files that you don't want to be included in your snapshot, since only files you previously chose will be in the staging area. In fact, that's precisely the point of the staging are--to allow you to selectively choose which files to include in your commit.&#x20;

## Cloning a Git Repository

Cloning a Git repository means making a copy of an existing repository. As such, it comes populated with the project files.

To clone a Git repository, follow these steps:

1. Obtain the Git URL of the repository you want to clone. A Git URL comes in many forms, depending on which transfer protocol you’re using. Assuming you’re cloning a repository from Github, you’re URL will be in the following format: &#x20;

| https://github.com/username/repository\_name.git |
| ------------------------------------------------ |

3. Clone the repository:

| git clone https://github.com/username/repository\_name.git |
| ---------------------------------------------------------- |

\
Replace the URL with the one you copied from the remote repository. This command will create the directory repository\_name in the current working directory.







## Git workflow:



The local Git workflow can be summed up in the following diagram. Files in the workspace can be either tracked or untracked.&#x20;

Workspace

Staging area (.git directory)

Repository (.git directory)&#x20;
