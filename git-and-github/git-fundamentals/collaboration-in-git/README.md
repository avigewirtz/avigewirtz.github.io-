# Collaboration in Git

Software development is a collaborative process, often involving multiple team members working together on a codebase. For example, in COS217 you will work on several of the assignments with a partner. In such an environment, you and your partner will often need to sync up your personal repositories with each other. While it is theoretically possible for each of you to sync up your personal repositories directly with each other, this approach is not ideal for many reasons.&#x20;

Instead, the standard approach in Git is to (1) sync up your repositories via an intermediate repository that neither of you directly develop in; and (2) to host the intermediate repository on a server like GitHub. Your workflow might look like the following:

1. At the beginning of the project, one member makes a copy of the assignment repository on their personal GitHub account.&#x20;
2. You add your partner as a collaborator.&#x20;
3. Each of you clones the repository to your development computer (i.e., armlab).&#x20;
4. When either of you has a material change to the code, you upload it to the GitHub repository, thereby syncing up the two repositories.&#x20;
5. Your partner downloads the updates from the shared repository, syncing up their personal repository as well. &#x20;
6. Repeat steps 4-5 as necessary.&#x20;
7. When the assignment is completed, submit it on armlab.&#x20;

In this context, the shared repository is called a remote repository, while the repositories you are developing are called local repositories.&#x20;

In Git jargon, uploading content to a remote repository is called pushing, while downloading content from a remote repository is called pulling.&#x20;

{% hint style="info" %}
Note that a "local" repository need not be located on your "local" computer, and a "remote" repository need not be located on a remote computer. In fact, in COS217 your repository on armlab is your "local" repository, even though armlab is a "remote" computer.&#x20;

A repository's classification as local or remote is (1) not indicative of its physical location; and (2) not indicative of its function. It is only a meaningful term when describing the relationship between two or more repositories from the perspective of one of them. I will illustrate this with an example. Say you and your partner's repositories are both located on the same computer (e.g., armlab), and your repositories both exchange data directly between each other--instead of via an intermediate repository on GitHub. (While this is poor practice, it is theoretically possible.) Which one of these repositories would you classify "local" and which one would you classify as "remote"? It depends! From your perspective, your repository is "local," since it is the one you're developing in, and your partner's repository is "remote," since it is the one you're exchanging data with. From your partner's perspective, however, the opposite is the case. the repository you're developing in is local, while your partner's repository is "remote." From your partner's perspective, however, their repository is "local," while yours is "remote."&#x20;
{% endhint %}

Pushing and pulling

The Git clone command is only the first step in sharing code. For these purposes, Git supports push and pull operations between repositories. \


Just like with the Git clone operation, a pull or push operation requires a URL. This tells Git where to locate the remote repository. A push or pull command might look like the following: &#x20;

\


git pull remote\_repo\_URL

git push remote\_repo\_URL

.&#x20;



&#x20;

\


<figure><img src="https://lh5.googleusercontent.com/V9qWq02Y1cNgFrJKH5LB3BcAxF-Xe1QMtuvWCbjiznxzTey1kIhW_wEsGdB4tQQNLdqAi7yFMpLGMy7yldDIeTsw8QUmghasKX6l7_VI6wkNI949454pPaCf8OnblwbH4Ma8l5FiiTYpxZYLA4GFTtU" alt=""><figcaption></figcaption></figure>



\
