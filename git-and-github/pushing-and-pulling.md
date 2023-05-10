# Pushing and Pulling

After cloning a repository, you may want to later sync up the two repositories. Git supports this through operations called _pushing_ (uploading) and _pulling_ (downloading). Pushing and pulling are accomplished with the `git push` and `git pull` commands, respectively.&#x20;

Just like when you Git needed a URL when you cloned a Git repository, Git also needs a URL  for pushing or pulling with a repository. As such, a push or pull operation takes a URL as an argument:

```bash
git push https://github.com/GITHUB_USERNAME/REPOSITORY_NAME.git
git pull https://github.com/GITHUB_USERNAME/REPOSITORY_NAME.git
```

### Remotes

However, Git has this neat feature called _remotes_, which saves you from typing lengthy URLs. A remote is simply an alias for a URL, allowing you to subsequently refer to the source as "origin" instead of its full URL. With a remote, a Git Push or Pull operation might instead be invoked like so:

```bash
git push ALIAS_NAME
git pull ALIAS_NAME
```

When you clone a Git repository, Git automatically saves the source repository's URL in an alias named _origin_. There is nothing special about origin. It is an arbitrary choice by Git, and you can change the the name if you'd like (though you'd probably not want to, since the name origin is so standard). With this in mind, push or pull operations from a clone to the source repository might look like the following:

```bash
git push origin 
```

In fact, it's even simpler; you don't even need to provide "origin" as an argument when interacting with the source repository, since Git defaults to origin when no argument is provided. Thus, you can simply invoke:

```bash
git push
git pull
```

and Git will use the origin as the argument.&#x20;

Note that a repository can have any number of remotes, allowing you to do pull or push operations with multiple remote repositories.&#x20;

## Git Workflow with Remotes

The addition of remotes adds another layer to the Git workflow, as shown below.&#x20;

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
When exchanging data with another repository, the repository you are working in is called the local repository, while the repository you are exchanging data with is called the remote repository. However, it is important to note that there is no fundamental difference between a "local" and "remote" repository.

A repository's classification as local or remote is (1) not inherently indicative of its physical location or (2) its function. The terms "local" and "remote" are only meaningful when describing the relationship between two or more repositories from the perspective of one of them. I will illustrate this with a (somewhat extreme) example. Say you and your partner both clone a repository to armlab. Either assume that your repositories exchange data directly with each other--that is, instead of via an intermediate repository on GitHub. (While this is poor practice, it is theoretically possible.) Which one of these repositories would you classify "local" and which one would you classify as "remote"?&#x20;

As far as physical location goes, both repositories on located on a remote computer--armlab.&#x20;

As far as function goes, it depends on perspective. From your perspective, your repository is "local," since it is the one you're developing in, and your partner's repository is "remote," since it is the one you're exchanging data with. From your partner's perspective, however, the opposite is the case. the repository you're developing in is local, while your partner's repository is "remote." From your partner's perspective, however, their repository is "local," while yours is "remote."

In sum, the terms local and remote are meaningful when describing the relationship between two repositories from the perspective of one of them. The repository you're working in is considered "local," irrespective of its location, and the repository you're exchanging data with is considered "remote," irrespective of its physical location.&#x20;
{% endhint %}
