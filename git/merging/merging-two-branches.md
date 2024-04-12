# How merging works

We will demonstrate how merging works via examples.&#x20;

## Fast-forward merge

we have a repository with one commit that contains one file: names.txt.&#x20;

<figure><img src="../../.gitbook/assets/Group 125.png" alt="" width="188"><figcaption></figcaption></figure>



We create a new branch named test, switch to test, and make a couple of commits. Over the course of the two commits, we make the following changes:

1. change Bob on line 2 of names.txt to Ben
2. Add a new file named hello.txt and write the word "hello" in it

The updated state is shown in Figure 21.

<figure><img src="../../.gitbook/assets/Group 127 (1).png" alt="" width="375"><figcaption></figcaption></figure>

then we change back to main and invoke 'git merge test':

<figure><img src="../../.gitbook/assets/Group 124 (1).png" alt="" width="375"><figcaption></figcaption></figure>





## 3-Way Merge



<figure><img src="../../.gitbook/assets/Group 154 (1).png" alt="" width="563"><figcaption></figcaption></figure>





AFTER MERGE

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



To fix the conflicts,&#x20;

To resolve&#x20;

1. Decide whether hello.txt should be kept or deleted
2.

{% code title="names.txt" lineNumbers="true" %}
```
Alex
Alice
<<<<<<< HEAD
Ben
Colin
=======
Claire
>>>>>>> test
Derek
Evan
Fred
```
{% endcode %}

