# Fast-Forward Merge Example

we have a repository with one commit that contains one file: names.txt.&#x20;

<figure><img src="../../.gitbook/assets/Group 125.png" alt="" width="188"><figcaption></figcaption></figure>



We create a new branch named test, switch to test, and make a couple of commits. Over the course of the two commits, we make the following changes:

1. change Bob on line 2 of names.txt to Ben
2. Add a new file named hello.txt and write the word "hello" in it

The updated state is shown in Figure 21.

<figure><img src="../../.gitbook/assets/Group 127 (1).png" alt="" width="375"><figcaption></figcaption></figure>

then we change back to main and invoke 'git merge test':

<figure><img src="../../.gitbook/assets/Group 124 (1).png" alt="" width="375"><figcaption></figcaption></figure>

h
