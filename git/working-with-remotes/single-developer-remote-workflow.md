# Single-developer remote workflow

Current repository:

<figure><img src="../../.gitbook/assets/Group 192 (1).png" alt="" width="563"><figcaption></figcaption></figure>

steps:

* create repository on github
* create a "connection" via remote&#x20;
* change master branch name on local repo to main so it mathes github
* now push. we can all branches or just one or more. we'll start off by pushing just main and then show how to push all branches at once.&#x20;

## Create Github repo:

<figure><img src="../../.gitbook/assets/Group 208.png" alt="" width="563"><figcaption></figcaption></figure>

## Adding GitHub repository as a remote:

```
git remote add origin https://github.com/avigewirtz/hello2.git
```

technically optional. purely convinience thing. benefit of origin is no need to specify URL.&#x20;

Establishes one way relationship

<figure><img src="../../.gitbook/assets/Group 209.png" alt="" width="563"><figcaption></figcaption></figure>

#### Showing Your Remotes <a href="#showing_your_remotes" id="showing_your_remotes"></a>

## Renaming master to main

<figure><img src="../../.gitbook/assets/Group 210.png" alt="" width="563"><figcaption></figcaption></figure>

## First time push:

The first time you push a branch, the general form is as follows:

```
git push -u REMOTE_NAME LOCAL_BRANCH_NAME
```

In our case, the remote name is origin, and the branch we want to push is main. So we invoke:

```
git push -u origin main
```

Git transfers the commits on main to the origin repository. Git would then perform a fast-forward merge operation on the

* couple of interesting things happen.

<figure><img src="../../.gitbook/assets/Group 211.png" alt="" width="563"><figcaption></figcaption></figure>

Explain what the -u option does and expain the remote tracking branch that's now a part of our repository.&#x20;



* do git log



## Making commit and pushing again

suppose we not make a couple of local commits. invoke git status. show how it's ahead two commits.&#x20;

<figure><img src="../../.gitbook/assets/Group 216.png" alt="" width="563"><figcaption></figcaption></figure>

we can push the main branch again, but this time we don't need to supply a remote name or branch name:

```
git push
```

<figure><img src="../../.gitbook/assets/Group 221.png" alt="" width="563"><figcaption></figcaption></figure>

## Pushing all branches

Suppose we want to push all branches.&#x20;

```
git push -u -all
```

The effect is that out local and remote repositories are currently in full sync. And now a remote trackoing branch will be created for test, named origin/test.&#x20;

<figure><img src="../../.gitbook/assets/Group 217.png" alt="" width="563"><figcaption></figcaption></figure>

