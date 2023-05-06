# Obtaining COS217 Assignment Repositories

Now that we’ve discussed the basics of how Git works, let’s delve into the specifics of obtaining COS217 assignment repositories. All assignment repositories are hosted on the COS217 GitHub account. In COS217, you will want to maintain two copies of each COS217 assignment repository. One copy on your (or your partner’s) GitHub account, and one copy on your development computer. Further, you will want your development repository to be linked to your repository on GitHub.&#x20;

While the process for obtaining two copies is seemingly straightforward, it is somewhat complicated by the fact that by default, Git links a clone to its source. Thus, if you clone the official COS217 repository to your development computer, the clone will be linked to the COS217 repository. This is not what you want, however. You want the clone to be linked to your personal GitHub copy.&#x20;

There are numerous ways you can get around this. We will now cover two methods. The first method is much simpler, but it uses the GitHub Import Tool, which is not native to Git.  The second method is more complex, but it uses native Git commands. &#x20;

## Method 1: Using the GitHub Import Tool

Method 1 involves two steps:&#x20;

1. Duplicate the original COS217 GitHub repository to your personal GitHub account.&#x20;
2. Clone the duplicate to your development computer.&#x20;

### Import the Git repository to your GitHub account&#x20;

The GitHub import tool can be used to duplicate any Git repository located on the Internet to your personal GitHub account. The imported repository will be uploaded as an independent copy, devoid of any links to the original. In the following example, we will import the assignment 0 Survey repository to your GitHub account.&#x20;

* Browse to https://github.com/new/import and sign into your account. (You can also reach this page by going to the GitHub homepage, signing into your account, then clicking on the plus sign at the top right of the page and choosing Import Repository.)
* Fill in the COS 217 assignment repository URL in the input box labeled Your old repository’s clone URL. In this example, that would be: [https://github.com/COS217/Survey.git](https://github.com/COS217/Survey.git).&#x20;
* Choose your new repository’s name, select Private, and click Begin import. GitHub’s servers will do the work and email you when the import is complete.&#x20;

### Step 2: Clone the GitHub repository to your development computer&#x20;

To clone a GitHub repository to your development computer, you will use the git clone command. In the following evening, we will clone the assignment 0 Survey repository to your development computer.&#x20;

1. Login to your development computer. From the command line, navigate to the directory you want the repository to reside in using the cd command.&#x20;
2. Clone the repository by entering the following command: git clone https://github.com/yourGitHubUsername/Survey.git

You will now have a local copy of the Survey repository on your development computer.&#x20;

Important: make sure you clone the repository from your personal GitHub account, and not from the COS217 GitHub account. If you clone from the COS217 account, your local repository will not be linked to your copy on GitHub.

## Method 2: Using Git Commands

The second method is somewhat complicated and involves many more steps than the first method. The steps are as follows:

1. Clone the COS217 GitHub repository to your development computer.&#x20;
2. Create a new repository on GitHub.&#x20;
3. Upload the data from your local copy to your repository on GitHub.&#x20;
4. Clone your (updated) GitHub repository to your development computer&#x20;
5. (Optional) delete the bare clone&#x20;

