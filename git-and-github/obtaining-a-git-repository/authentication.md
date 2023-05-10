# Authentication

When you clone a Git repository, you will sometimes need to provide credentials to prove that you are authorized to access the repository. In the previous example (i.e., when we cloned _survey_ from GitHub), we did not need to provide authentication credentials, since the repository was _public_--meaning it can be viewed and cloned by anyone.

It goes without saying that when you upload a repository to GitHub, you don't necessarily want to make it visible to the world. As such, Github provides you the option of classifying your repository as _private_. Private repositories are only visible to their owner(s) and explicitly invited collaborators. Thus, when attempting to clone a private repository, you need to first authenticate yourself. You do so by providing the GitHub username and password of an authorized account. However, instead of using the regular login password, you will need to use a [Personal Access Token](../../appendices/git-installation.md#generating-a-github-personal-access-token), which provides enhanced security measures.

{% hint style="warning" %}
Note that when uploading data to a repository--the process of which we'll cover soon--you need to authenticate for both public and private repositories.&#x20;
{% endhint %}

The following diaram illustrates the possible directions of file transfers between the relevant COS217 computers and acccounts:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-01 at 2.35.17 PM.png" alt=""><figcaption></figcaption></figure>
