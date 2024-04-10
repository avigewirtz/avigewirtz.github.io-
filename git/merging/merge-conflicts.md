# Merge conflicts



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

## Resolving conflicts

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
