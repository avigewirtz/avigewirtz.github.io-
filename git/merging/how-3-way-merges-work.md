# How 3-Way Merges Work

3 way merges can be successful or result in a conflict. we will demonstrate how merging works and when conflicts arise via an example.&#x20;

## Starting point

<figure><img src="../../.gitbook/assets/Group 124 (1).png" alt="" width="563"><figcaption></figcaption></figure>



## Diverging history

<figure><img src="../../.gitbook/assets/Group 154 (1).png" alt="" width="563"><figcaption></figcaption></figure>



## Merging

<figure><img src="../../.gitbook/assets/Group 160.png" alt=""><figcaption></figcaption></figure>

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

