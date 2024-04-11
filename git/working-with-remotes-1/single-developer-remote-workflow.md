# Single-developer remote workflow

Current repository:

<figure><img src="../../.gitbook/assets/Group 192 (1).png" alt="" width="563"><figcaption></figcaption></figure>

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

<figure><img src="../../.gitbook/assets/Group 211.png" alt="" width="563"><figcaption></figcaption></figure>

Typical practice is to push only branch you're working on.&#x20;

The first time you push a a single branch, the general form is as follows:

```
git push -u REMOTE_NAME LOCAL_BRANCH_NAME
```

Remote name is the name of the remote you want to push to. In our case that's origin. local branch name is the branch we want to push. In our case that's main.&#x20;

In our case, thats:

```
git push origin main
```

Git would transfer your commits to the origin repository and add them to the history at B. Git would then perform a fast-forward merge operation on the

* couple of interesting things happen.



If you wanted to push your X and Y commits upstream at this point, you could do so easily. Git would transfer your commits to the origin repository and add them to the history at B. Git would then perform a fast-forward merge operation on the main branch, putting in your edits and updating the ref to point to Y.&#x20;





* remote tracking branch: does not move. can't change to it. remote a bit of a misnohmer.&#x20;



## Making commit and pushing again

<figure><img src="../../.gitbook/assets/Group 216.png" alt="" width="563"><figcaption></figcaption></figure>

* invoke git status. show how it's ahead two commits.&#x20;

<figure><img src="../../.gitbook/assets/Group 221.png" alt="" width="563"><figcaption></figcaption></figure>

## Pushing all branches

```
git push -all
```



* benefit or upstream branch is no need to state branch

<figure><img src="../../.gitbook/assets/Group 217.png" alt="" width="563"><figcaption></figcaption></figure>
