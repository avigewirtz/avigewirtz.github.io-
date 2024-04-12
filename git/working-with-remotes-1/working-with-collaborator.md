# Multi-developer remote workflow

When a remote repository is shared by multiple developers, as is the typical case, its adds a layer of complexity to development. Now, you have multiple people pushing and pulling.&#x20;



we'll go over workflow with two developers.&#x20;



* Step 1: add partner as collaborator&#x20;



* step 2: partner clones repository&#x20;

the branch that `HEAD` points to in the remote repository will be the branch that is initially checked out in Ben's clone. In our case, HEAD points to main.&#x20;



* name of the repository on github is names.git here's what cloning does:

{% hint style="success" %}
**Git clone under the hood**

Git clone is actaully a wrapper around other commands. When you invoke git clone, the following is done by git behind the scenes:

* Creates a new directory named `repo`.
* Initializes a Git repository in that directory by running `init`.
* Sets a new remote named `origin` pointing to `https://github.com/example/repo.git`.
* Fetches all the data from `repo`.&#x20;
* Checks out the default branch of `repo` into your new local directory. The default branch is the branch in the remote repository that HEAD points to.&#x20;
{% endhint %}





## Scenario 1: one partner pushes new commits



* invoke git status. says up to date. not accurate.&#x20;
* you pull. essentially fetch and merge



## Scenario 2:&#x20;





## Scenario 3: merge conflict





On the other hand, suppose another developer had already pushed some commits to the origin repository, and the result looked more like Figure 11-5 when you attemp‐ ted to push your history up to the origin repository. In effect, you are attempting to cause your history to be sent to the shared repository when there is already a different history there. The origin history does not simply fast-forward from B. This situation is called the non-fast-forward push problem.

When you attempt your push, Git rejects it and tells you about the conflict with a message like this:

$ git push\
To /tmp/Depot/my\_website

! \[rejected] main -> main (non-fast forward) error: failed to push some refs to '/tmp/Depot/my\_website'

So what are you really trying to do? Do you want to overwrite the other developer’s work, or do you want to incorporate both sets of histories?

If you want to overwrite all other changes, you can! Simply use the -f option on your git push. We just hope you won’t need that alternate history!

More often, you are not trying to wipe out the existing origin history but just want your own changes to be added. In this case, you must perform a merge of the two histories in your repository before pushing.
