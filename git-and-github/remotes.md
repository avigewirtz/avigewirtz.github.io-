# Remotes

When we cloned the repository Survey, we provided Git with a URL so it could locate the repository. It is&#x20;



it is standard for each project ton contain at least two repositories. to work with two repositories have a&#x20;

To clone a Git repository, you need to provide Git a URL. After cloning a repository,&#x20;

As you can imagine, providing lengthy URLs everytime you wish to interact with a remote repository is tedious. Thus, to make things easier, Git can store the URLs of any number of remote repositories you are interested in names, or aliases, which are easier to remember.&#x20;

In fact, when you clone a Git repository, Git automatically stores the URL of the source repository in an alias named origin. Thus, after a clone operation, you can simply reference the source repository using “origin” instead of its URL.&#x20;

To simplify things further, Git defaults to origin whenever a remote isn’t supplied in a push or pull operation on the command line. Thus, a “git push/pull” is equivalent to git push/pull origin.&#x20;

Note that the relationship between a local and remote repository  is (by default) a one-way relationship. The remote repository has no knowledge of nor does it maintain a link to the local one.&#x20;





&#x20;\--the GitHub username whether you are cloning a repository from your own GitHub account or from someone else's account.&#x20;



represents the Note that the GitHub username can represent your personal username or someone else's.&#x20;

For example, to clone the Survey repository for assignment 0, you'd replace GITHUB\_USERNAME with :&#x20;

```bash
git clone https://github.com/cos217/survey.git
```

\


Replace the URL with the one you copied from the remote repository. This command will create the directory repository\_name in the current working directory.

