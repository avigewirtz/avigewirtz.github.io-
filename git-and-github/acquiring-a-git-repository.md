# Acquiring a Git Repository

```bash
git clone https://github.com/avigewirtz/git_practice.git && cd git_practice && rm -rf .git && cd ..
```

There are two ways you can acquire a Git repository:&#x20;

1. You can create a new Git repository.&#x20;
2. You can copy an existing Git repository.

## Creating a Git Repository

Creating a repository means initializing a repository for a project that is not currently under Git version control. For example, say your home directory contains directory the _git\_practice_ with the following contents: _README.md_, hello.c, _cirle1.c_ and _circle2.c._&#x20;



The process of creating a Git repository is extremely simple. You simply navigate (using the cd command) to the directory containing the files you wish to version control and invoke git init. This will create a hidden .git subdirectory that contains all the information needed to version-control your project. Note that creating a Git repository (i.e., invoking git init) does not in itself cause all the files in that directory to be saved to the Git repository. As we’ll discuss later, you must manually add each file you want git to track to the repository.

## Cloning a Git Repository

Cloning a Git repository means making a copy of an existing repository. Unlike a new repository, a cloned repository comes with all project files, history, and other metadata from the source repository. Some information, however—such as configuration settings— is not propagated from to the cloned repository. &#x20;

A repository can be cloned from anywhere, be it from the same computer or a from one connected over a network. In practice, however, repositories are generally cloned from popular hosting platforms like GitHub, Gitlab, and Bitbucket.&#x20;

To clone a Git repository, follow these steps:

\


1. Obtain the Git URL of the repository you want to clone. A Git URL comes in many forms, depending on which transfer protocol you’re using. Assuming you’re cloning a repository from Github, you’re URL will be in the following format: &#x20;

| https://github.com/username/repository\_name.git |
| ------------------------------------------------ |

Where username represents the GitHub username of the account you want to clone from and repository\_name represents the name of the repository. You can find the URL by going to the repository page on Github and clicking the “Code” button.&#x20;

2. On the command line, navigate to the directory you want the cloned repository to reside in:

| cd pathToDirectory |
| ------------------ |

3. Clone the repository:

| git clone https://github.com/username/repository\_name.git |
| ---------------------------------------------------------- |

\
Replace the URL with the one you copied from the remote repository. This command will create the directory repository\_name in the current working directory.

