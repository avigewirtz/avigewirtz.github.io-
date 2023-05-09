# COS217 Development Workflow



Software development is a collaborative process, often involving multiple team members working together on a codebase. For example, in COS217 you will work on several of the assignments with a partner. In such an environment, you and your partner will often need to sync up your personal repositories with one another, ensuring you both have the same version of code.&#x20;

While it is theoretically possible for each of you to sync up your personal repositories directly with each other via push or pull operations, as shown in Figure X, this approach is not ideal for many reasons.&#x20;

<figure><img src="../.gitbook/assets/image (10) (1).png" alt="" width="319"><figcaption></figcaption></figure>

Instead, the standard approach is to (1) sync up your repositories via an intermediate repository that neither of you directly develop in; and (2) to host the intermediate repository on a server like GitHub. This workflow is called the _centralized workflow_.&#x20;

<figure><img src="../.gitbook/assets/image (8) (1).png" alt="" width="319"><figcaption></figcaption></figure>

Using this approach, your workflow might look like the following:

1. When beginning an assignment, either you or your partner copies the assignment repository from the COS217 GitHub account to their personal GitHub account and adds their partner as a collaborator. This repository will serve as the shared repository. &#x20;
2. Each of you clones the repository to your development computer (e.g., armlab).&#x20;
3. When either of you makes a material update to the code, you push (upload) it to the GitHub repository, thereby syncing up the two repositories.&#x20;
4. Your partner pulls (downloads) the updates from the shared repository, syncing up their personal repository as well. &#x20;
5. Repeat steps 4-5, until you complete the assignment.&#x20;
6. Submit the assignment on armlab.&#x20;









After you obtain the repositories, you will be ready&#x20;



On individual assignments:

<figure><img src="../.gitbook/assets/Screenshot 2023-05-01 at 2.35.35 PM.png" alt=""><figcaption></figcaption></figure>

On partnered assignments:

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2023-05-01 at 2.35.17 PM.png" alt=""><figcaption></figcaption></figure>
