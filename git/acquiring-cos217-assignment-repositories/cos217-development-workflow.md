# COS217 Development Workflow

Your workflow in COS217 will depend on several factors, such as whether the assignment is an individual or partnered assignment and whether you develop on Armlab or your personal computer. Below we provide an illustration of the COS217 workflow for both individual and partnered assignments. The illustrations assume you are developing on Armlab.&#x20;

### Workflow on Individual Assignments

On individual assignments, your workflow might look like the following:

1. When beginning the assignment, you import the assignment repository from the COS217 GitHub account to your personal GitHub. &#x20;
2. You clone your GitHub repository to Armlab.&#x20;
3. When you are finished developing, you (in any order):
   1. Submit your assignment to the COS217 Armlab account.
   2. Synchronize your local repository with your remote copy on GitHub.

This workflow is illustrated in the following diagram:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-01 at 2.35.35 PM.png" alt=""><figcaption></figcaption></figure>

### Workflow on Partnered Assignments

In COS217 you will work on several of the assignments with a partner. In such an environment, you and your partner will often need to sync up your personal repositories with one another, ensuring you both have the same version of code.&#x20;

While it is theoretically possible for each of you to sync up your personal repositories directly with each other via push or pull operations, as shown in the figure below, this approach is not ideal for many reasons.&#x20;

<figure><img src="../../.gitbook/assets/image (10) (1).png" alt="" width="319"><figcaption></figcaption></figure>

Instead, the standard approach is to (1) sync up your repositories via an intermediate repository that neither of you directly develop in; and (2) to host the intermediate repository on a server like GitHub. This workflow is called the _centralized workflow_.&#x20;

<figure><img src="../../.gitbook/assets/image (8) (1).png" alt="" width="319"><figcaption></figcaption></figure>

Using this approach, your workflow might look like the following:

1. When beginning an assignment, you and your partner copy the assignment repository from the COS217 GitHub account to your personal GitHub account.
2. One partner invites the other partner as a collaborator. This repository will serve as your shared repository. &#x20;
3. Both partners clone the GitHub repository to Armlab.&#x20;
4. When either partner makes a material update to the code, they push (upload) their changes to GitHub, thereby synchronizing their local copy with the shared repository.&#x20;
5. The other partner pulls (downloads) the updates from the shared repository, synchronizing their local copy with the shared copy. All three repositories are now synchronized.  &#x20;
6. Repeat steps 4-5 as necessary. until you complete the assignment.&#x20;
7. When the assignment is complete, one partner submits it to the COS217 Armlab account.&#x20;

This workflow is illustrated in the following diagram:

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>
