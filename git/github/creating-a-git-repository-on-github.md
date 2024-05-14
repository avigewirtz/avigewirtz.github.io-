# Creating a Git Repository on GitHub

1. [Sign in ](https://github.com/)to GitHub. You should see the following box on the front page: ![](<../../.gitbook/assets/Screenshot 2024-04-05 at 1.32.52 PM.png>)
2. We'll name the repository "remotePractice," choose **Private**, and click **Create a New Repository**.&#x20;
3.  On the resulting page, copy the URL:&#x20;

    <figure><img src="../../.gitbook/assets/Screenshot 2024-04-05 at 1.54.08 PM.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Clone under the hood**

essentially a sequence of several commands. Can't do this here because i haven't covered pull or push yet. also, might have to do collaboration workflowe since i can't demonstarte pull otherwise
{% endhint %}





It goes without saying that when you upload a repository to GitHub, you don't necessarily want to make it visible to the world. As such, Github provides you the option of classifying your repository as _private_. Private repositories are only visible to their owner(s) and explicitly invited collaborators. As such, when someone attempts to clone a private repository, they need to provide authenticate credentials by providing a password. Note that this password is not the standard account password but a [Personal Access Token](broken-reference).

{% hint style="warning" %}
When _uploading_ data to a repository, you need to authenticate yourself irrespective of whether the repository is public or private.
{% endhint %}

The following diagram illustrates the permissible directions for file transfers between the relevant COS217 computers and accounts:
