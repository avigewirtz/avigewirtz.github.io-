# Cloning a Git Repository

\
Cloning a Git repository means making a copy of an existing repository. The clone comes populated with the source repository's files, history, and other metadata.  To process of cloning a repository is straightforward. You simply invoke the `git clone` command followed by the repository's URL. For example, to clone a repository from GitHub, run:

```bash
git clone https://github.com/GITHUB_USERNAME/REPOSITORY_NAME.git
```

The value for GITHUB\_USERNAME will depend on which GitHub account the source repository is located on. For example, if the source repository is located on the COS217 GitHub account, the username would be COS217. If it is located on your personal account, the username would be your personal GitHub username. Let's now clone the Assignment 0 Survey repository, which is stored on the COS217 GitHub account:&#x20;

```bash
git clone https://github.com/cos217/survey.git
```

Upon success, you will get the following output:

<figure><img src="../.gitbook/assets/Screenshot 2023-05-04 at 8.00.49 PM (1).png" alt=""><figcaption></figcaption></figure>

## Authentication

When we cloned the Survey repository from the COS217 GitHub account, we did not need any authentication credentials. That is because the Survey repository is _public_. A public repository can be viewed and cloned by anyone.&#x20;

It goes without saying that when you upload a repository to GitHub, you don't necessarily want to make it public to the world. As such, you have the option of classifying your repository as either _private_. Private repositories are only visible to their owner(s) and explicitly invited collaborators.&#x20;

To clone a private repository, you need to authenticate yourself. You do so by providing the username and password. However, note that this password is not the login password, but a Personal Access Token, which offers more robust security.&#x20;

## Working Tree

GitHub repositories are typically _bare_. A bare repository is a repository with no associated working tree.&#x20;

When you clone the bare repository from GitHub, Git automatically creates a directory with the same name as the source repository, places the git repository in a .git subdirectory, and checks out the latest version (i.e., commit) of all project files. &#x20;

For example, when you clone _survey.git_, Git creates a directory named Survey, puts the Git repository in a subdirectory named .git, and then checks out the latest version to the workspace.&#x20;



<figure><img src="../.gitbook/assets/image (9) (1).png" alt="" width="375"><figcaption></figcaption></figure>

##

