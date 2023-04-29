# Collaborative Workflows

In a team-based environment, although it is theoretically possible for developers to exchange data directly with each other directly via their local repositories, as shown in Figure X, this method is not ideal for many obvious reasons.

\


<figure><img src="https://lh3.googleusercontent.com/B-he8w3fyrNG4aXKNiPdgRfF7lfiV7BkVjbRVpHTS4oH8Nn1PgJom5xyGweJeptiDBSuK6tbKDIUPsC70rXvuJwXCL-dtRMXLCIqQ_2b7iUjgzwM6ILrZMAcigVsMe_8pTgN9NfmDbYbipADPyVcV3Y" alt=""><figcaption></figcaption></figure>

\


Instead of communicating with other developers via your local repository, the preferred method for collaboration is to communicate with other developers via an intermediate repository located on a server that all developers have access to.&#x20;

\


Even in such an arrangement (I.e., where developers communicate via intermediate repositories), there are still many workflows that are possible with Git. A common collaboration model is the centralized workflow. (You are encouraged to use this model for partnered COS217 assignments.)

\
\


3.5.1 Centralized workflow

\


The centralized workflow is a collaboration model in which there is a central repository, typically hosted on a server like GitHub, that all developers have access to, as shown in Figure X. This repository contains the main codebase that serves as the authoritative version of the project; as such, it is the repository that all team members synchronize their code with.&#x20;

&#x20;

\


<figure><img src="https://lh5.googleusercontent.com/V9qWq02Y1cNgFrJKH5LB3BcAxF-Xe1QMtuvWCbjiznxzTey1kIhW_wEsGdB4tQQNLdqAi7yFMpLGMy7yldDIeTsw8QUmghasKX6l7_VI6wkNI949454pPaCf8OnblwbH4Ma8l5FiiTYpxZYLA4GFTtU" alt=""><figcaption></figcaption></figure>

\


A highly simplified workflow sequence using  this collaboration model might look like the following:

\


1. Each developer clones the shared repository to their development computer. They will use the copy to develop with.&#x20;
2. When a developer is ready to share their changes, they upload, or push, their changes to the central repository. This makes the changes visible to other team members and allows them to review, test, and provide feedback. Note that at this step the changes are not yet merged into the main codebase.&#x20;
3. If the changes are approved, they are merged into the main codebase. This step may involve resolving any merge conflicts that arise due to concurrent changes made by other developers. We will discuss merge conflicts later and how to resolve them.&#x20;
4. After the All team members download, or pull, the updated changes to their local repositories. From here steps 2-4 are repeated.
