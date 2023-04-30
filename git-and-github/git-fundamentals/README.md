# Git Fundamentals

Before issuing Git commands, it's important to have a high-level overview of how Git works. &#x20;

## Git repositories

“A Git repository is simply a database containing all the information needed to retain and manage the revisions and history of a project.” The repository is typically stored at the root of your project’s workspace in a hidden directory named .git.

Within the .git directory, there are many files and subdirectories, each containing important repository information. A few highlights of what is contained in the .git directory:&#x20;

* A copy of all files under Git version control&#x20;
* A record of the changes made to the files at various stages of development. Included in this record is:
  * The names of the authors who made the changes&#x20;
  * Timestamps of the changes&#x20;
* References or links to other repositories that your repository might be interested in communicating with. This will be elaborated on in the section on remotes.&#x20;
* A configuration file containing repository-specific information, such as the repository user's name and email address.&#x20;
