# Pushing and Pulling

You will often want to sync up two repositories, particularly a clone with its source. Git supports this through operations called _pushing_ (uploading) and _pulling_ (downloading), which are accomplished via the `git push` and `git pull` commands respectively.&#x20;

Just like Git needs a URL to clone a remote repository, Git needs a URL to push to or pull from a remote repository. As such, the syntax for git push and git pull looks like the following:&#x20;

```bash
git push https://github.com/GITHUB_USERNAME/REPOSITORY_NAME.git
git pull https://github.com/GITHUB_USERNAME/REPOSITORY_NAME.git
```

## Remotes

Git has this neat feature called _remotes_, which is simply an alias for a URL, that saves you from typing lengthy URLs every time you want to push or pull. With a remote, the syntax for a push or pull operation might look like the following:

```bash
git push ALIAS_NAME
git pull ALIAS_NAME
```

Where ALIAS\_NAME is a variable that holds the value of the remote repository's URL. A repository can have any number of remotes, allowing you to do pull or push operations with multiple remote repositories.&#x20;

## Origin

When you clone a Git repository, Git automatically saves the source repository's URL in an alias named _origin_. There is nothing special about origin--it is an arbitrary name, and you can change it if you'd like (though you'd probably not want to). When you invoke git push or pull without supplying a URL or alias, Git defaults to origin. Thus, you can do push or pull operations with a source repository as follows:&#x20;

```bash
git push
git pull
```

and Git will use automatically add origin as the argument.&#x20;

## Git Workflow with Remotes

The addition of remotes adds another layer to the Git workflow--the "remote repository," as shown in the figure below.&#x20;

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
When exchanging data with another repository, the repository you are working in is called the local repository, while the repository you are exchanging data with is called the remote repository. However, it is important to note that there is no fundamental difference between a "local" and "remote" repository.

A repository's classification as local or remote is (1) not inherently indicative of its physical location or (2) its function. The terms "local" and "remote" are only meaningful when describing the relationship between two or more repositories from the perspective of one of them. I will illustrate this with a (somewhat extreme) example. Say you and your partner both clone a repository to Armlab. Further say that your repositories exchange data directly with each other--that is, instead of via an intermediate repository on GitHub. (While this is poor practice, it is theoretically possible.) Which one of these repositories would you classify as "local" and which one would you classify as "remote"?&#x20;

As far as physical location goes, both repositories on located on a remote computer--Armlab.&#x20;

As far as function goes, it depends on perspective. From your perspective, your repository is "local," since it is the one you're developing in, and your partner's repository is "remote," since it is the one you're exchanging data with. From your partner's perspective, however, the opposite is the case. the repository you're developing in is local, while your partner's repository is "remote." From your partner's perspective, however, their repository is "local," while yours is "remote."

In sum, the terms local and remote are meaningful when describing the relationship between two repositories from the perspective of one of them. The repository you're working in is considered "local," irrespective of its location, and the repository you're exchanging data with is considered "remote," irrespective of its physical location.&#x20;
{% endhint %}
