# Collaborative workflows

##



Until this point, we've worked entirely within a single repository. One of the core features of Git is it's support for collaborative workflows. That is, a workflow consisting of multiple programmers, each with their own working copy of the project, and enabling them to sync up their work.&#x20;

in context of data exchange, repository youre working in is local and other is remote.&#x20;

## Distributed VCS



<figure><img src="../../.gitbook/assets/Group 44 (2).png" alt="" width="375"><figcaption></figcaption></figure>

For many reasons, however, this is a bad idea. However, even in a distributed system, still use centralized that nobody works in. such as repository is called a bare repository. simply means it has no working tree.

PUSHING/FETCHING



<figure><img src="../../.gitbook/assets/Group 45 (2).png" alt="" width="375"><figcaption></figcaption></figure>



As we stated earlier, in a typical collaborative workflow with Git, each developer has their own local copy of the repository, and they all sync up their repositories via a central repository located on some server.&#x20;

The most common place to host Git repositories is GitHub. In such a workflow, the central repository is uploaded to github perhaps in an organization account or perhaps in one of the collaborastors accounts. GitHub is accessible 24/7 and offers many features that aid on top of Git. In this tuturial, won't focus much on github.&#x20;

<figure><img src="../../.gitbook/assets/Group 57 (1).png" alt="" width="375"><figcaption></figcaption></figure>

## Creating a Git repository on GitHub



* when it comes to github, you need to know
  * how to create a git repository on github
  * how to authenticate with github on the command line
  * how to add a collaborator

## Authentication

It goes without saying that when you upload a repository to GitHub, you don't necessarily want to make it visible to the world. As such, Github provides you the option of classifying your repository as _private_. Private repositories are only visible to their owner(s) and explicitly invited collaborators. As such, when someone attempts to clone a private repository, they need to provide authenticate credentials by providing a password. Note that this password is not the standard account password but a [Personal Access Token](../background/git-installation.md#generating-a-github-personal-access-token).

{% hint style="warning" %}
When _uploading_ data to a repository, you need to authenticate yourself irrespective of whether the repository is public or private.
{% endhint %}

The following diagram illustrates the permissible directions for file transfers between the relevant COS217 computers and accounts:
