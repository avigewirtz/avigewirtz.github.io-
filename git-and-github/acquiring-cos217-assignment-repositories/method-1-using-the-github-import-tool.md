# Method 1: Using the GitHub Import Tool

Method one involves two steps:&#x20;

1. Duplicate the original COS217 GitHub repository to your personal GitHub account.&#x20;
2. Clone the duplicate to your development computer.&#x20;

Step 1 can be accomplished with the GitHub import tool, while step 2 is accomplished with the Git clone command. We will now briefly explain the GitHub import tool and the git clone command, demonstrating both by using assignment 0. \\

### Step 1: Import the Git repository to your GitHub account&#x20;

The Github import tool can be used to duplicate any Git repository located on the Internet to your personal GitHub account. The imported repository will be uploaded as an independent copy, devoid of any links to the original. In the following example, we will import assignment 0 Survey repository to your GitHub account.&#x20;

* Browse to https://github.com/new/import and sign into your account. (You can also reach this page by going to the GitHub homepage, signing into your account, then clicking on the plus sign at the top right of the page and choosing Import Repository.)
* Fill in the COS 217 assignment repository URL in the input box labeled Your old repository’s clone URL. In this example, that would be: [https://github.com/COS217/Survey.git](https://github.com/COS217/Survey.git).&#x20;
* Choose your new repository’s name, select Private, and click Begin import. GitHub’s servers will do the work and email you when the import is complete.&#x20;

\


### Step 2: Clone the GitHub repository to your development computer&#x20;

To clone a GitHub repository to your development computer, you will use the git clone command. In the following evening, we will clone the assignment 0 Survey repository to your development computer.&#x20;

1. Login to your development computer. From the command line, navigate to the directory you want the repository to reside in using the cd command.&#x20;
2. Clone the repository by entering the following command:

| git clone https://github.com/yourGitHubUsername/Survey.git |
| ---------------------------------------------------------- |

You will now have a local copy of the Survey repository on your development computer.&#x20;

Important: make sure you clone the repository from your personal GitHub account, and not from the COS217 GitHub account. If you clone from the COS217 account, your local repository will not be linked to your copy on GitHub.

\
\
