# Recording Changes to the Repository

Now that we understand the components of a Git project, let's dive into the details of recording changes to the repository. One of the key commands we'll be using is `git status`. This command compares the working tree to the index and the index to the latest commit, reporting any changes. At this point, if we invoke `git status`, it'll tell us that our working tree is "clean":

<figure><img src="../../.gitbook/assets/Screenshot 2024-04-04 at 5.10.37 PM.png" alt=""><figcaption></figcaption></figure>

There are four common scenarios that can make our working tree "dirty": modifying a file, adding a new file, deleting a file, and renaming a file. Let's explore each one.

**Modifying a File**

Suppose we modify `hello.txt` by appending "world" to it:

```
echo "world" >> hello.txt
```

Now, let's check the status:

```bash
~/git_playground$ git status
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   hello.txt

no changes added to commit (use "git add" and/or "git commit -a")
~/git_playground$
```

We see that `hello.txt` is listed under "Changes not staged for commit" as "modified." Git compares `hello.txt` in our working tree to the version of `hello.txt` in the index and sees that they're different. To include the modified version in our next commit, we need to add it to the index:

```bash
git add hello.txt
```

Let's check the status again:

```bash
~/git_playground$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   hello.txt

~/git_playground$
```

Now `hello.txt` is still listed as "modified," but this time under "Changes to be committed." Git compares the version of `hello.txt` in the index to the version in the latest commit and reports that they're different. To save a snapshot of the contents in the index, we run:

```
~/git_playground$ git commit -m "appended 'world' to hello.txt"
[main 66ee698] appended 'world' to hello.txt
 1 file changed, 1 insertion(+)
~/git_playground$ 
```

**Modifying a Staged File**

Let's say we now modify `hi.txt` and stage it:

```
~/git_playground$ echo "there" >> hi.txt
~/git_playground$ git add hi.txt 
```

When we check the status, we'll see `hi.txt` listed as "modified" under "Changes to be committed":

```
~/git_playground$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   hi.txt

~/git_playground$ 
```

Now, suppose that instead of committing, we modify `hi.txt` again, this time appending "world" to it:

```
~/git_playground$ echo "world" >> hi.txt
```

When we check the status again, we see something interesting. `hi.txt` is listed as modified under both "Changes to be committed" and "Changes not staged for commit":

```git
~/git_playground$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   hi.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   hi.txt

~/git_playground$
```

What's going on here? If you're following what we discussed earlier about Git copying the file's contents when you stage the file, this makes sense. The version of `hi.txt` that was staged first contains "there," but the working tree version now contains "there" and "world." Git tracks both versions separately: the staged version and the working tree version.

**Adding a New File**

Let's say we want to add a new file to our project. We'll create a new file called `greeting.txt`:

```bash
echo "hello, world" > greeting.txt
```

Now, let's check the status:

```bash
~/git_playground$ git status
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	greeting.txt

nothing added to commit but untracked files present (use "git add" to track)
~/git_playground$
```

We see that `greeting.txt` is listed under "Untracked files." This means Git knows about the file, but it’s not being tracked yet. To understand this better, let's compare it to a modified file.

When a file is **modified**, a version of it already exists in the index. When you change this file, Git compares the current version in your working tree to the version in the index and reports that the file is "modified."

With an **untracked** file like `greeting.txt`, however, Git doesn’t have a reference for this file in the index. This means Git isn’t monitoring its contents. If you modify an untracked file, Git won't know about the changes because it’s not tracking the file’s contents yet.

To start tracking `greeting.txt` and include it in our next commit, we need to add it to the index:

```bash
git add greeting.txt
```

Now, let's check the status again:

```bash
~/git_playground$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   greeting.txt
~/git_playground$
```

We see that `greeting.txt` is now listed under "Changes to be committed" as a "new file." This means it has been added to the index and will be included in the next commit. To save a snapshot of the index, including our new file, we run:

```bash
git commit -m "added greeting.txt with a friendly message"
```

You should see a message like this:

```bash
[main 5d41402] added greeting.txt with a friendly message
 1 file changed, 1 insertion(+)
 create mode 100644 greeting.txt
~/git_playground$
```

Now, our repository includes the new file `greeting.txt`, and the commit history has been updated to reflect this addition.

**Modifying Another New File After Staging**

Let's create another new file called `farewell.txt` and add some text to it:

```bash
echo "goodbye, world" > farewell.txt
```

Now, let's check the status:

```bash
~/git_playground$ git status
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	farewell.txt

nothing added to commit but untracked files present (use "git add" to track)
~/git_playground$
```

We see that `farewell.txt` is listed under "Untracked files." Let's add it to the index:

```bash
git add farewell.txt
```

Now, let's check the status again:

```bash
~/git_playground$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   farewell.txt
~/git_playground$
```

Now `farewell.txt` is listed under "Changes to be committed" as a "new file." This means it has been added to the index and will be included in the next commit.

What happens if we modify `farewell.txt` after adding it to the index? Let's append more text to it:

```bash
echo "see you later" >> farewell.txt
```

Now, let's check the status again:

```bash
~/git_playground$ git status
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   farewell.txt

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   farewell.txt

~/git_playground$
```

We see that `farewell.txt` is now listed under both "Changes not staged for commit" and "Changes to be committed." This is because Git compares the current version of `farewell.txt` in the working tree to the version in the index and sees that they are different.

To include the modified version of `farewell.txt` in our next commit, we need to add it to the index again:

```bash
git add farewell.txt
```

Now, let's check the status again:

```bash
~/git_playground$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   farewell.txt
~/git_playground$
```

Now `farewell.txt` is listed under "Changes to be committed" as "modified." This means the updated version is now staged for the next commit.

To save a snapshot of the updated index, including our modified file, we run:

```bash
git commit -m "appended 'see you later' to farewell.txt"
```

You should see a message like this:

```bash
[main 8b6b5c1] appended 'see you later' to farewell.txt
 1 file changed, 1 insertion(+)
~/git_playground$
```

By understanding how to add new files, modify them, and track these changes in Git, you can effectively manage your project’s history and ensure all important changes are recorded accurately.

**Deleting a File**



<mark style="color:red;">Removing a File</mark>

<mark style="color:red;">$ git rm filename</mark>

<mark style="color:red;">Changing the Index | 49</mark>

<mark style="color:red;">This does two things:</mark>

1. <mark style="color:red;">Deletes the file’s entry from the index, scheduling it for re‐ moval in the next commit</mark>
2. <mark style="color:red;">Deletes the working file as well, as with rm filename</mark>



Now, let's see what happens when we delete a file in our project. We'll delete the `hi.txt` file.

First, let's check the current status to see the files in our project:

```bash
~/git_playground$ ls
bye  greeting.txt  hello.txt  hi.txt  farewell.txt
```

To delete `hi.txt`, we can use the `rm` (remove) command:

```bash
rm hi.txt
```

Now, let's check the status again:

```bash
~/git_playground$ git status
On branch main
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	deleted:    hi.txt

no changes added to commit (use "git add" and/or "git commit -a")
~/git_playground$
```

We see that `hi.txt` is listed under "Changes not staged for commit" as "deleted." What does this mean? Git compares the working tree to the index. Even though we deleted `hi.txt` from the working tree, it still exists in the index. This discrepancy is what Git reports as a "deleted" file.

If we don't stage the deleted file, it won't be included in the next commit. This makes sense if you understand that the index maintains an independent copy of the file—the version at the time you staged it. The index isn't automatically updated to reflect the working tree changes unless you explicitly stage those changes.

To stage the deletion of `hi.txt`, we need to use the `git rm` command. This tells Git to track the file deletion:

```bash
git rm hi.txt
```

Alternatively, if we had used `git rm hi.txt` instead of `rm hi.txt`, it would have deleted the file and staged the deletion in one step. Let's demonstrate this by recreating and deleting the file using `git rm`:

First, recreate `hi.txt`:

```bash
echo "hi" > hi.txt
git add hi.txt
git commit -m "recreated hi.txt"
```

Now, let's use `git rm` to remove and stage the deletion in one step:

```bash
git rm hi.txt
```

Let's check the status again:

```bash
~/git_playground$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	deleted:    hi.txt
~/git_playground$
```

Now `hi.txt` is listed under "Changes to be committed" as "deleted." This means the deletion has been staged and will be included in the next commit.

To save a snapshot of the index, including the deletion of `hi.txt`, we run:

```bash
git commit -m "deleted hi.txt using git rm"
```

You should see a message like this:

```bash
[main d47f1c3] deleted hi.txt using git rm
 1 file changed, 0 insertions(+), 0 deletions(-)
 delete mode 100644 hi.txt
~/git_playground$
```

Now, our repository has been updated to reflect the deletion of `hi.txt`. By understanding how to delete files and track these changes in Git, you can manage your project’s history effectively, ensuring that all important changes, including deletions, are recorded accurately.

**Renaming a File**

Let's see what happens when we rename a file in our project. We'll rename the `hello.txt` file to `greetings.txt`.

First, let's check the current status to see the files in our project:

```bash
~/git_playground$ ls
bye  farewell.txt  greeting.txt  hello.txt
```

To rename `hello.txt` to `greetings.txt`, we can use the `mv` (move) command:

```bash
mv hello.txt greetings.txt
```

Now, let's check the status:

```bash
~/git_playground$ git status
On branch main
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	renamed:    hello.txt -> greetings.txt

no changes added to commit (use "git add" and/or "git commit -a")
~/git_playground$
```

We see that the file is listed under "Changes not staged for commit" as "renamed: hello.txt -> greetings.txt." This means Git has detected the renaming of the file but hasn't staged the change yet.

To stage the renaming of `hello.txt` to `greetings.txt`, we use the `git add` command:

```bash
git add greetings.txt
```

Alternatively, we can use `git mv` instead of `mv` to rename the file and stage the change in one step:

```bash
git mv hello.txt greetings.txt
```

Let's undo the previous rename and use `git mv` for demonstration:

First, undo the previous rename:

```bash
mv greetings.txt hello.txt
git add hello.txt
git commit -m "restored hello.txt"
```

Now, let's use `git mv` to rename and stage the change in one step:

```bash
git mv hello.txt greetings.txt
```

Let's check the status again:

```bash
~/git_playground$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	renamed:    hello.txt -> greetings.txt
~/git_playground$
```

Now, `hello.txt` is listed under "Changes to be committed" as "renamed: hello.txt -> greetings.txt." This means the renaming has been staged and will be included in the next commit.

To save a snapshot of the index, including the renaming of the file, we run:

```bash
git commit -m "renamed hello.txt to greetings.txt"
```

You should see a message like this:

```bash
[main e7d1c8a] renamed hello.txt to greetings.txt
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename hello.txt => greetings.txt (100%)
~/git_playground$
```

Now, our repository has been updated to reflect the renaming of `hello.txt` to `greetings.txt`. By understanding how to rename files and track these changes in Git, you can manage your project’s history effectively, ensuring that all important changes, including renames, are recorded accurately.
