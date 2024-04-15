# Merge examples

Examples using&#x20;

## Fast-forward merge

We have a repository with a single commit that includes one file: `names.txt`.&#x20;

<figure><img src="../../.gitbook/assets/Group 246.png" alt="" width="162"><figcaption></figcaption></figure>

First, we create a new branch called `test` and switch to it:

```bash
git branch test
git checkout test 
```

<figure><img src="../../.gitbook/assets/Group 249.png" alt="" width="188"><figcaption></figcaption></figure>

On the `test` branch, we make a couple of commits. First, we modify `names.txt` by changing "Bob" on line 2 to "Ben":

```bash
sed -i 's/Bob/Ben/' names.txt
git add names.txt
git commit -m "Changed Bob to Ben"
```

Next, we add a new file named `hello.txt` and write the word "hello" in it:

```bash
echo "hello" > hello.txt
git add hello.txt
git commit -m "Added hello.txt"
```

The repository now reflects these changes, as shown in Figure 21.

<figure><img src="../../.gitbook/assets/Group 127 (2).png" alt="" width="375"><figcaption></figcaption></figure>

We now switch back to the `master` branch:

```bash
git checkout master
```

<figure><img src="../../.gitbook/assets/Group 243 (1).png" alt="" width="375"><figcaption></figcaption></figure>

To incorporate the changes from the `test` branch into `main`, we use the `git merge` command:

```bash
git merge test
```

Since main and test haven't diverged, all Git has to do to merge them is move the main branch forward two commits to C3:

<figure><img src="../../.gitbook/assets/Group 250.png" alt="" width="375"><figcaption></figcaption></figure>

This sort of merge is known as a fast forward merge. Is it a case of a degenerate merge, since no real sense of merging occurs.&#x20;



## 3-way merge

3 way merges can be successful or result in a conflict. we will demonstrate via an example how 3-way merges merging works and when conflicts arise.&#x20;

## Starting point

We'll start off by continuing from the state of our repository in the fast forward merge example.&#x20;

<figure><img src="../../.gitbook/assets/Group 250.png" alt="" width="563"><figcaption></figcaption></figure>



## Diverging history

On the master branch we make the following two changes followed by a commit:

1. we add the name "fred" to the end of names.txt
2. we create a new file named bye.txt and write bye in it

<figure><img src="../../.gitbook/assets/Group 253.png" alt="" width="563"><figcaption></figcaption></figure>

Then we switch to the test branch and make a few changes followed by a commit.&#x20;

1. Change "alice" to "alex"&#x20;
2. Delete "ben"&#x20;
3. create a new file hi.txt and write hi in it

<figure><img src="../../.gitbook/assets/Group 255.png" alt="" width="563"><figcaption></figcaption></figure>



## Merging&#x20;

To merge test into master, we switch back into master:

```
git checkout master
```

and invoke:

```
git merge test
```

The merged version will be stored as a new commit. Hence, git prompt us for a commit message in our preffered text editor. Simply enter the message and&#x20;

Master will point to C6, since since test was merged into it, while test will remain pointing where it is, at C5. &#x20;

<figure><img src="../../.gitbook/assets/Group 278.png" alt=""><figcaption></figcaption></figure>

## How 3-way merge works

When we ask Git to merge, we're asking git it to figure out which parts of the commits each branch points to include or delete. At first glance, it may seem that asking Git to merge these two branches is too much to ask.&#x20;

The precise algorithm Git uses by default is complex and full cobvergae is beyond the scope of this tutorial. As a general rule, we can break it down into two parts.&#x20;

1. determining which files should be included
2. determining which parts of each file should be included

$$A_1$$= $$A_2$$



## Merge conflict











CASE 3:



<figure><img src="../../.gitbook/assets/Group 163 (1).png" alt=""><figcaption></figcaption></figure>

marge fails

```bash
~/gitnames2> git status
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Changes to be committed:
	new file:   hi.txt

Unmerged paths:
  (use "git add/rm <file>..." as appropriate to mark resolution)
	deleted by us:   hello.txt
	both modified:   names.txt

~/gitnames2> 
```

This tells us that two of the files could not be merged by git: hello.txt and names.txt. For hello.txt, the issue is that it was "deleted by us" (us meaning our branch--masster), but it was modified on the other branch. Git has no way of knowing whether we want to keep the the modified version or keep it deleted.&#x20;

For names.txt, the issue is that both branches modified the same unit of it.&#x20;

We have two options:

1. Abort the merge by invoking `git merge --abort`, and git will take us back to the state of the repository before the merge was attempted.&#x20;
2. Complete the merge by fixing conflicts and committing.&#x20;

