# Obtaining COS217 Assignment Repositories

Now that we’ve discussed the basics of how Git works, let’s delve into the specifics of obtaining COS217 assignment repositories. All COS217 assignment repositories are hosted on the [COS217 GitHub account](https://github.com/orgs/COS217/repositories). You will want to maintain two copies of each such repository. One copy to keep on GitHub, and one copy to keep on your development computer. Further, you want your development repository to be linked to your repository on GitHub.&#x20;

While the process for obtaining two such copies is seemingly straightforward, it is somewhat complicated by the fact that in Git, when you clone a repository, the clone is by default automatically linked to the source via a [remote](broken-reference). Thus, if you clone the official COS217 repository directly to your development computer, the clone will be linked to the official COS217 repository. This is not what you want, however. You want the clone to be linked to your personal GitHub repository.&#x20;

There are numerous ways you can get around this. Two methods are covered in COS217. The first method is much simpler, but it uses the GitHub Import Tool, which is not native to Git. The second method is more complex, but it uses native Git commands. In this tutorial, we will only cover the First method. If you're interested in learning about the second method, you can refer to the Git & GitHub Primer handout.&#x20;

## Method 1: Using the GitHub Import Tool

Method 1 involves two steps. Importing the repository to your GitHub account, then cloning it to your development computer. These examples will assume that armlab is your development computer.

#### Step 1: Duplicate the repository to your GitHub account

You can duplicate the repository with the GitHub Import Tool, which creates an independent copy of the repository on your GitHub account, devoid of any connection to the original. In the following example, we will import the assignment 0 Survey repository to your GitHub account.&#x20;

1. Browse to https://github.com/new/import and sign into your account. (You can also reach this page by going to the GitHub homepage, signing into your account, then clicking on the plus sign at the top right of the page and choosing _Import Repository_.)
2. Fill in the repository URL in the input box. In our example, the URL is `https://github.com/COS217/Survey.git`.&#x20;
3. Under **Your new repository details**, input your desired repository name, (e.g., _Survey_), select **Private**, then click **Begin import**.&#x20;
4. **Partnered assignments only**: Invite your partner as a collaborator.&#x20;
   * Go to your repository page and click **Settings**. On the lefthand sidebar, click **Collaborators** and then click **Add people**. Input your partner's GitHub username and click the **Add** button.

#### Step 2: Clone the GitHub repository to armlab

Log into armlab and clone the repository:

<pre class="language-bash"><code class="lang-bash">git clone https://github.com/<a data-footnote-ref href="#user-content-fn-1">YOUR_GITHUB_USERNAME</a>/Survey.git
</code></pre>

You will now have a copy of the Survey repository on your development computer that is linked to your copy on GitHub.&#x20;



[^1]: Your personal username (i.e., not COS217!)
