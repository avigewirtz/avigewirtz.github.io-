# Fast-Forward Merge

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
