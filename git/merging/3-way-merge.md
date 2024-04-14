# 3-Way Merge

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

When we ask Git to merge, we're asking git it to figure out which parts of the commits each branch points to include or delete. At first glance, it may seem that asking Git to merge these two branches is too much to ask. How is it supposed to know what to include and not include? For example, Git sees that C4 has the file bye.txt, which is not contained in C5. Conversely, C5 contains hello.txt and hit.txt, which are not in C4. How is Git supposed to know which if any of these three files should be in the merge? Thankfully, Git has more information that just the two branches alone. It uses the most recent common ancestor to glean a signifigant amount of information. In our case, that's C4.&#x20;

The precise algorithm Git uses by default is complex and full cobvergae is beyond the scope of this tutorial. As a general rule, we can break it down into two parts.&#x20;

1. determining which files should be included
2. determining which parts of each file should be included

$$A_1$$= $$A_2$$



#### Determining which files to in include

Consider file A. Version in C3 will be denoted A\_C3&#x20;

* case 1: Agreement between C3 and C4 for file A:\


Easy case: there is agreement between C3 and C4.&#x20;

* A file in c3 was deleted in both.&#x20;
* Contents of $$A_{C4} = A_{C5}$$. They could be new, modified,&#x20;

$$A_{C4}$$= $$A_{C5}$$

This would be the case if

This would be the case if both are unmodified or if both are modified identically or if both were created.

* File A unmodified in both.&#x20;
* File A modified identically in both.&#x20;
* File A deleted in both.&#x20;
* Case 2: disagreement between C3 and C4 for file A:

$$A_1 \neq A_2$$

Case 1 one modofied, the other unmodified:

$$A = A_1 \neq A_2 \Rightarrow A_2$$

$$A = A_2 \neq A_1 \Rightarrow A_1$$

$$A \neq A_1 \neq A_2 \Rightarrow merge(A_1 + A_2)$$

$$B \neq A_1 \neq A_2 \Rightarrow conflict$$

$$A \neq B \neq A_2 \Rightarrow conflict$$

$$B \neq A_1 \neq B \Rightarrow A_1$$

$$B \neq B \neq A_2 \Rightarrow A_2$$



$$nonexistent \neq A_1 \neq A_2 \Rightarrow conflict$$

Case 3:&#x20;

$$A_1$$deleted, $$A_2$$unmodified -> $$A_1$$

$$A_2$$deleted, $$A_1$$unmodified -> $$A_2$$

$$A_1$$deleted, $$A_2$$modified -> $$conflict$$

$$A_2$$deleted, $$A_1$$modified -> $$conflict$$

* $$A_1 \neq A_2$$. $$A = A_1 \neq A_2$$then $$A_2$$is used. $$A = A_2 \neq A_1$$then $$A = A_1 \neq A_2$$
* File A modified in both. we'll call the them A' and A''. A' does not equal A''. attempts to merge A' and A''. Will discusss how this is done soon.&#x20;
* &#x20;can succeed or fail. Will cover this soon. File modified in one and unmodified in other other: modified version included. File unmodified in one and deleted in other: delete included. File modified in one and deleted in other. Conflict.&#x20;



#### Determining which parts of each file to include&#x20;





| C3  | C4 - C5          | C6 |
| --- | ---------------- | -- |
| N/A | $$A_1 = A_2$$    |    |
| A   | $$A_1 \neq A_2$$ |    |
|     |                  |    |



* easy case: contents of both files are identical.&#x20;





<figure><img src="../../.gitbook/assets/Group 274.png" alt="" width="563"><figcaption></figcaption></figure>





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

