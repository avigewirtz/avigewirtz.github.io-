# Authentication

When you clone a Git repository, you will sometimes need to provide credentials to prove that you are authorized to access the repository. In the previous example (i.e., when we cloned _survey_ from GitHub), we did not need to provide authentication credentials, since the repository was _public_--meaning it can be viewed and cloned by anyone.

It goes without saying that when you upload a repository to GitHub, you don't necessarily want to make it visible to the world. As such, Github provides you the option of classifying your repository as _private_. Private repositories are only visible to their owner(s) and explicitly invited collaborators. As such, when someone attempts to clone a private repository, they need to provide authenticate credentials by providing a password. Note that this password is not the standard account password but a [Personal Access Token](../git-installation.md#generating-a-github-personal-access-token).

{% hint style="warning" %}
When _uploading_ data to a repository, you need to authenticate yourself irrespective of whether the repository is public or private.
{% endhint %}

The following diagram illustrates the permissible directions for file transfers between the relevant COS217 computers and accounts:

<figure><img src="../../../.gitbook/assets/Screenshot 2023-05-01 at 2.35.17 PM.png" alt=""><figcaption></figcaption></figure>
