# Cloning a Git Repository

\
Cloning a Git repository means making a copy of an existing repository. The clone comes populated with the source repository's files, history, and other metadata. &#x20;

To process of cloning a repository is extremely simple. You simply invoke:

```bash
git clone SOURCE_REPOSITORY_URL
```

The source repository URL tells Git where to locate the repository. The repository can theoretically be hosted on any computer; for practical purposes, however, it's typically hosted on publicly accessible servers like GitHub, GitLab, or GitBucket. In COS217, all assignment repositories are hosted on GitHub; therefore, all examples will assume that.

The URL for a GitHub-hosted repository looks like the following:

```bash
git clone https://github.com/GITHUB_USERNAME/REPOSITORY_NAME.git
```

The value for GITHUB\_USERNAME will depend on which GitHub account the source repository is on. For example, if the source repository is located on the COS217 GitHub account, the username would be cos217. If it is located on your personal account, the username would be your personal GitHub username. Let's now clone the Survey repository for assignment 0:

```bash
git clone https://github.com/cos217/survey.git
```

The output will look like the following:

<figure><img src="../.gitbook/assets/Screenshot 2023-05-04 at 8.00.49 PM (1).png" alt=""><figcaption></figcaption></figure>

Before moving forward, now is a good time to discuss two important concepts--remotes, and authentication.&#x20;

## Authentication

It goes without saying that when you upload a repository to GitHub, you don't necessarily want to make it public to the world. As such, you have the option of classifying your repository as either _public_ or _private_. Public repositories are visible to everyone on the Internet, and their contents can be cloned by anyone. In contrast, private repositories are only visible to their owner(s) and explicitly invited collaborators.&#x20;

In the previous example, we were able to clone Survey since it's a public repository. However, if we had tried to clone a private repository--such as another student's COS217 assignment repository--you'd have been prompted for login credentials. For example, lets try to clone the following private repository:

```bash
git clone https://github.com/avigewirtz/private_repo.git
```

You will be prompted for a passcode, which of course you do not have, and the clone will fail:

<figure><img src="../.gitbook/assets/Screenshot 2023-05-04 at 8.29.51 PM.png" alt=""><figcaption></figcaption></figure>

Note that the password you are prompted for is not the GitHub account's regular login password, but a Personal Access Token, which offers more robust security.&#x20;
