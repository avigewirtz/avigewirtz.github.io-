# Workflow with remotes

Our workflow will look like the following:

* Create Git repository on GitHub
*

## Creating a Git repository on GitHub

1. First, we [Sign in ](https://github.com/)to GitHub. You should see the following box on the front page: ![](<../../.gitbook/assets/Screenshot 2024-04-05 at 1.32.52 PM.png>)
2. We'll name the repository "remotePractice," choose **Private**, and click **Create a New Repository**.&#x20;
3.  On the resulting page, copy the URL:&#x20;

    <figure><img src="../../.gitbook/assets/Screenshot 2024-04-05 at 1.54.08 PM.png" alt=""><figcaption></figcaption></figure>

## Cloning a git repository

The second step is to get a copy of the repository we just created on GitHub. To do so, we navigate to the directory we want the clone to reside in and invoke `git clone` with the source repository's URL as an argument. In our case, we'll invoke git clone in the home directory:

```bash
cd
git clone https://github.com/avigewirtz/remotePractice.git
cd remotePractice
```

authentication





{% hint style="info" %}
**Clone under the hood**

essentially a sequence of several commands. Can't do this here because i haven't covered pull or push yet. also, might have to do collaboration workflowe since i can't demonstarte pull otherwise
{% endhint %}





















When you clone a Git repository, you will sometimes need to provide credentials to prove that you are authorized to access the repository. In the previous example (i.e., when we cloned _survey_ from GitHub), we did not need to provide authentication credentials, since the repository was _public_--meaning it can be viewed and cloned by anyone.

It goes without saying that when you upload a repository to GitHub, you don't necessarily want to make it visible to the world. As such, Github provides you the option of classifying your repository as _private_. Private repositories are only visible to their owner(s) and explicitly invited collaborators. As such, when someone attempts to clone a private repository, they need to provide authenticate credentials by providing a password. Note that this password is not the standard account password but a [Personal Access Token](../background/git-installation.md#generating-a-github-personal-access-token).

{% hint style="warning" %}
When _uploading_ data to a repository, you need to authenticate yourself irrespective of whether the repository is public or private.
{% endhint %}

The following diagram illustrates the permissible directions for file transfers between the relevant COS217 computers and accounts:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-01 at 2.35.17 PM.png" alt=""><figcaption></figcaption></figure>

