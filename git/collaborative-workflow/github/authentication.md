# Authentication

It goes without saying that when you upload a repository to GitHub, you don't necessarily want to make it visible to the world. As such, Github provides you the option of classifying your repository as _private_. Private repositories are only visible to their owner(s) and explicitly invited collaborators. As such, when someone attempts to clone a private repository, they need to provide authenticate credentials by providing a password. Note that this password is not the standard account password but a [Personal Access Token](../../background/git-installation.md#generating-a-github-personal-access-token).

{% hint style="warning" %}
When _uploading_ data to a repository, you need to authenticate yourself irrespective of whether the repository is public or private.
{% endhint %}

The following diagram illustrates the permissible directions for file transfers between the relevant COS217 computers and accounts:
