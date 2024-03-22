# Obtaining COS217 Assignment Repositories

Now that we’ve discussed the basics of how Git works, let’s delve into the specifics of obtaining COS217 assignment repositories. All COS217 assignment repositories are hosted on the [COS217 GitHub account](https://github.com/orgs/COS217/repositories). You will want to maintain two copies of each such repository--one "remote" copy on GitHub, and one "local" copy on your development computer. You also want the local copy to be linked to the remote one, ensuring you can seamlessly sync up the two.&#x20;

While the process for obtaining two such copies is seemingly straightforward, it is somewhat complicated by the fact that in Git, when you clone a repository, the clone is by default linked to the source via a [remote](broken-reference). Thus, if you clone the official COS217 repository directly to your development computer, the clone will be linked to the official COS217 repository. This is not what you want--you want the clone to be linked to your personal GitHub copy.&#x20;

There are numerous ways you can get around this. Two methods are covered in COS217. The first method is much simpler, but it uses the GitHub Import Tool, which is not native to Git. The second method is more complex, but it uses native Git commands. In this tutorial, we will only cover the first method, since it is much simpler. If you're interested in learning about the second method, you please refer to the Git & GitHub Primer handout.&#x20;

<details>

<summary>Step 1: Import the GitHub repository</summary>

The GitHub Import tool allows you to duplicate any GitHub repository, which creates an independent copy of the repository, devoid of any connection to the original. In the following example, we will import the assignment 0 Survey repository to your GitHub account.&#x20;

1. Browse to [https://github.com/new/import](https://github.com/new/import) and sign into your account.(You can also reach this page by going to the GitHub homepage, signing into your account, then clicking on the plus sign at the top right of the page and choosing _Import Repository_.)
2. Fill in the repository URL in the input box. For the Survey repository, the URL is `https://github.com/COS217/Survey.git`.&#x20;
3. Under **Your new repository details**, input your desired repository name, (e.g., _Survey_), <mark style="color:red;">select</mark> <mark style="color:red;"></mark><mark style="color:red;">**Private**</mark>, then click **Begin import**.&#x20;

### **Partnered assignments**

On partnered assignments only, complete the following steps to invite your partner as a collaborator. Note that only one partner needs to complete these steps.

1. Go to your repository page and click **Settings**.&#x20;
2. On the lefthand sidebar, click **Collaborators**, then click **Add people**.&#x20;
3. Input your partner's GitHub username and click the **Add** button.

</details>

#### Step 2: Clone the GitHub repository to Armlab

Log into Armlab and issue the following command:

<pre class="language-bash"><code class="lang-bash">git clone https://github.com/<a data-footnote-ref href="#user-content-fn-1">YOUR_GITHUB_USERNAME</a>/Survey.git
</code></pre>

You will now have a copy of the Survey repository on Armlab that is linked to your copy on GitHub.&#x20;



[^1]: Your personal username (i.e., not COS217!)
