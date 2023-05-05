# Collaboration in Git

Software development is a collaborative process, often involving multiple team members working together on a codebase. For example, in COS217 you will work on several of the assignments with a partner. In such an environment, you and your partner will often need to sync up your personal repositories with one another, ensuring you both have the same version of code.&#x20;

While it is theoretically possible for each of you to sync up your personal repositories directly with each other via push or pull operations, this approach is not ideal for many reasons. Instead, the standard approach is to (1) sync up your repositories via an intermediate repository that neither of you directly develop in; and (2) to host the intermediate repository on a server like GitHub. Using this approach, your workflow might look like the following:

1. When beginning an assignment, either you or your partner copies the assignment repository from the COS217 GitHub account to their personal GitHub account and adds their partner as a collaborator. This repository will serve as the shared repository. &#x20;
2. Each of you clones the repository to your development computer (e.g., armlab).&#x20;
3. When either of you makes a material update to the code, you push (upload) it to the GitHub repository, thereby syncing up the two repositories.&#x20;
4. Your partner pulls (downloads) the updates from the shared repository, syncing up their personal repository as well. &#x20;
5. Repeat steps 4-5, until you complete the assignment.&#x20;
6. Submit the assignment on armlab.&#x20;







{% hint style="info" %}
When exchanging data with another repository, the repository you are working in is called the local repository, while the repository you are exchanging data with is called the remote repository. However, it is important to note that there is no fundamental difference between local and remote repositories.

Note that a "local" repository need not be located on your "local" computer, and a "remote" repository need not be located on a remote computer. In fact, in COS217 your repository on armlab is your "local" repository, even though armlab is a "remote" computer.&#x20;

A repository's classification as local or remote is (1) not indicative of its physical location; and (2) not indicative of its function. It is only a meaningful term when describing the relationship between two or more repositories from the perspective of one of them. I will illustrate this with an example. Say you and your partner's repositories are both located on the same computer (e.g., armlab), and your repositories both exchange data directly between each other--instead of via an intermediate repository on GitHub. (While this is poor practice, it is theoretically possible.) Which one of these repositories would you classify "local" and which one would you classify as "remote"? It depends! From your perspective, your repository is "local," since it is the one you're developing in, and your partner's repository is "remote," since it is the one you're exchanging data with. From your partner's perspective, however, the opposite is the case. the repository you're developing in is local, while your partner's repository is "remote." From your partner's perspective, however, their repository is "local," while yours is "remote."&#x20;
{% endhint %}



.&#x20;



&#x20;

\


<figure><img src="https://lh5.googleusercontent.com/V9qWq02Y1cNgFrJKH5LB3BcAxF-Xe1QMtuvWCbjiznxzTey1kIhW_wEsGdB4tQQNLdqAi7yFMpLGMy7yldDIeTsw8QUmghasKX6l7_VI6wkNI949454pPaCf8OnblwbH4Ma8l5FiiTYpxZYLA4GFTtU" alt=""><figcaption></figcaption></figure>



\
