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

<figure><img src="../../.gitbook/assets/Group 277 (2).png" alt=""><figcaption></figcaption></figure>

The precise algorithm Git uses by default is complex and full cobvergae is beyond the scope of this tutorial. As a general rule, we can break it down into two parts.&#x20;

1. determining out which files should be included
2. determining which parts of each file should be included

#### Determining which files to in include

\<fill in>

* **Case 1: Agreement on file in C4 and C5. For example, File A appears in C4 and C5**. Include in C6. Does not even need to look at C3 to determine this. Similarly, if file A appears in C3 but not in C4 and C5, obvious not to include it.&#x20;
* Case 2: C4 and C5 do not agree. Two cases where this can happen:
  * File A in C4 but not C5. Looks at C3. If C3 contains A, A is not included in commit.&#x20;
  *

Harder cases:

* **Identical versions of File A appears in C3 and one other commit (C4 or C5), but it is either modified or deleted in the other.** In this case, the modified or deleted state is reflected in C6. Here are some examples:
  * C3 and C4 contain file _A_, but C5 contains _A'_ (modified version of A). _A'_ will be included in C6.&#x20;
  * C3 and C4 contain file _A_, but C5 does not (i.e., _A_ was deleted). _A_ will not be included in C6.&#x20;
*
* For example, identical versions of hello.txt appears in C3 and C5, but hello.txt is not in C4 (i.e., it was deleted). In this case, Git assumes you want the A deleted. Hence, it does not include A in C6.&#x20;
*

| C3 | C4  | C5  | C6                                                             |
| -- | --- | --- | -------------------------------------------------------------- |
| A  | A   | A   | A                                                              |
|    | A   | A   | A                                                              |
| A  |     |     |                                                                |
| A  | A   |     |                                                                |
| A  |     | A   |                                                                |
| A  | A'  | A'  | A'                                                             |
| A  | A'  | A   | A'                                                             |
| A  | A   | A'  | A'                                                             |
| A  | A'  |     | CONFLICT                                                       |
| A  |     | A'  | CONFLICT                                                       |
| A  | A'  | A'' | Attempts to merge A' and A''. Can succeed or produce conflict. |
| A  | A'' | A'  | Attempts to merge A' and A''. Can succeed or produce conflict. |

#### Determining which parts of each file to include&#x20;





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

