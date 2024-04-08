# Collaborative workflows

Until this point, we've worked entirely within a single repository. One of the core features of Git is it's support for collaborative workflows. That is, a workflow consisting of multiple programmers, each with their own working copy of the project, and enabling them to sync up their work.&#x20;







## Centralized VCS

One of the dominant models of VCS systems before Git was the centralized model. In a centralized workflow, everyone working on the project has their own working copy (i.e., working tree), but they all synchronize their work via a central repository on a server.&#x20;

<figure><img src="../../.gitbook/assets/Group 36 (6).png" alt="" width="375"><figcaption></figcaption></figure>

The key point in this arrangment is that each developer does have their own repository, which contains a complete compy is the project's history. Each developer has only a checked out version of the specific branch they're working on.&#x20;

## Distributed VCS

In contrast, Git (and most other current VCS's) is distributed. In this model, each developer has their own working tree, but they also each have their repository. Technically, each of them can synchronize their repositories directly.&#x20;

<figure><img src="../../.gitbook/assets/Group 44 (2).png" alt="" width="375"><figcaption></figcaption></figure>

For many reasons, however, this is a bad idea. However, even in a distributed system, Even in a distributed system



<figure><img src="../../.gitbook/assets/Group 45 (2).png" alt="" width="375"><figcaption></figcaption></figure>

## remote repository

A [repository](https://git-scm.com/docs/gitglossary#def\_repository) which is used to track the same project but resides somewhere else. To communicate with remotes, see [fetch](https://git-scm.com/docs/gitglossary#def\_fetch) or [push](https://git-scm.com/docs/gitglossary#def\_push).



## GitHub



A popular platform for hosting remote repositories
