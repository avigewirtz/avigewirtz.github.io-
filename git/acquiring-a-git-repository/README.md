# Beginner Local Workflow

There are two contexts in which version control is useful: personal use and collaborative use. Nowadays, almost all projects make use of some of Git's collaborative features. Even if your not actually working with someone else on the project, chances are you obtained your project by cloning somoene else's repository.&#x20;

In the first part of this tutorial, we'll go over using version control for personal use. All work contained within a single, local repository. We're doing it this way since it's simpler to explain.&#x20;

## The big picture

A simple local git workflow might look something like the following:

1. Set up a project by creating a new directory and populating it with files.&#x20;
2. Initialize a git repository in the root directory of the project
3. Save a first snapshot of the project to the git repository.&#x20;
4. Modify project by:
   1. Adding new files
   2. Modifying existing files
   3. Deleting files
5. Repeat steps 4-5.&#x20;

We'll go over each of these steps one by one. This should give you a good understanding of the basics of git. An important command we'll be using the throughout this section is the `git status`, which tells you the current state of your working tree and index.

## Creating the project

To create&#x20;

```
mkdir playground
cd playground
```

add a few files:

```
echo "hello" > hello.txt 
echo "hi" > hi.txt     
mkdir bye        
echo "bye" > bye/bye.txt
```



<figure><img src="../../.gitbook/assets/Group 118 (1).png" alt="" width="188"><figcaption></figcaption></figure>

## Initializing a repository

Simply invoke `git init` (short for initialize):&#x20;

```bash
~/playground> git init
Initialized empty Git repository in /Users/avigewirtz/playground/.git/
~/playground> 
```

If we invoke ls -l , we'll see that playground has a .git subdirectory:&#x20;

```bash
~/playground> \ls -A
.git    bye    hello.txt    hi.txt
~/playground>
```

<figure><img src="../../.gitbook/assets/Group 133.png" alt="" width="375"><figcaption></figcaption></figure>

The .git subdirectory is a skeleton repository. Essentially empty. As we mentioned in git in a nutshell, the repository contains tow main parts: the staging area and commit history. Since we just initialized the repository and haven't stages any files or made commits, both will be empty.&#x20;

<figure><img src="../../.gitbook/assets/Group 124.png" alt="" width="375"><figcaption></figcaption></figure>

## Saving a snapshot

The "index" holds a snapshot of the content of the working tree, and it

&#x20;      is this snapshot that is taken as the contents of the next commit. Thus

&#x20;      after making any changes to the working tree, and before running the

&#x20;      commit command, you must use the add command to add any new or modified

&#x20;      files to the index.

Recall that saving a snapshot is a two-step process. First we add the files we want to be in commit in the staging area, and then we commit, which captures all the files in the staging area. Basic form of stage command is as follows:

```
git add filenames
```

The filename can be a directory, in which case Git adds all the files descending from it as well. To stage all files in our project, we invoke:

```bash
git add hello.txt hi.txt bye
```

And now hello.txt, hi.txt, and bye.txt will be listed in the staging area (Figure 1-1). We can confirm this by invoking git status:

<figure><img src="../../.gitbook/assets/Group 129 (1).png" alt="" width="375"><figcaption></figcaption></figure>

#### Staging shortcuts

Recall that "." represents the working directory. Thus, to stage all changes in the working directory, simply invoke:&#x20;

```
git add .
```

```
git add -A
```

If you're in the root directory of your project, then these two commands are functionasly equivalent. &#x20;

### Committing

The general form of a Git commit command is as follows:

```bash
git commit -m "COMMIT_MESSAGE"
```

Where COMMIT\_MESSAGE is replaced with a concise, meaningful description of the changes you made. This message becomes a part of your commit and helps you (and potentially others) understand the purpose of the commit when reviewing the project's history. In our case, since it's our first commit and we don't have anything meaningful to say, we'll simply write "first commit" in the message spot:

<figure><img src="../../.gitbook/assets/Screenshot 2024-04-04 at 4.47.23 PM.png" alt="" width="563"><figcaption></figcaption></figure>

The result is that a snapshot of the current state of our project is now stored in the repository. For simplicity, we label this commit "commit 1," but as we'll see soon, commits are identified by a 40-digit hex number.&#x20;

<figure><img src="../../.gitbook/assets/Group 131.png" alt="" width="375"><figcaption><p>Figure 3: Our repository after the first commit.</p></figcaption></figure>

## Modifying the working tree <a href="#checking_status" id="checking_status"></a>

At this point, if we invoke git status, it'll tell us that our working tree is "clean":

<figure><img src="../../.gitbook/assets/Screenshot 2024-04-04 at 5.10.37 PM.png" alt=""><figcaption></figcaption></figure>

A clean working tree means that our working tree does not contain any new, modified or deleted files. In Git terminology, all the files in our working tree are "unmodified."&#x20;

if anything changes and we want to apply the changes, we will have to add the changes to the index. These modifications include:

* Creating a new file
* Modifying an existing file
* Deleting a file

Let's now make all three modifications to our working. First, let's modify hello.txt by appending "world" to it:

```
echo "world" >> hello.txt
```

Next, let's create a new file named hey.txt, and write "hey" in it:

```
echo "hey" >> hey.txt
```

finally, let's delete the file hi.txt:

```
rm -rf hi.txt
```

Invokig git status, we see that hello.txt is listed as modified, hey.txt as untracked, and hi.txt.&#x20;

Let's now examine the state of our working tree with Git status:&#x20;





The output tells us two things:

1. hello.txt was modified, and the modified version is not staged for commit.&#x20;
2. hey.txt is untracked











A perhaps pedantic but subtle point. Notice how we didn't have to add the unmodified files--hi.txt and bye.txt--to the staging area. We only had to stage hello.txt. This is because unmodified files are automatically in the staging area. This is a subtle point but will. When we invoke git status, it only lists the changes, but not unmodifies files.&#x20;



We see that the newly added file hey.txt is listed as "untracked." What happens is, git looks at the index, and sees no file with the name "hey.txt". (This is different that the previous example of. If a file is not in the index, then then not only is it not part of a previous commit, Git does not even track it. was it never part of In simple terms, an untracked file is one that is not in the staging area.  As we'll see soon, if you modify or delete an untracked file, Git won't&#x20;





{% hint style="info" %}
## When to commit



When working on your own, it’s useful to commit “early and often,” so that you can explore different ideas and make changes freely without worrying about recovering earlier work. Such commits are likely to be somewhat disorganized and have cryptic commit messages, which is fine because they need to be intelligible only to you, and for a short period of time. Once a portion of your work is finished and you’re ready to share it with others, though, you may want to reorganize those commits, to make them well-factored with regard to reusability of the changes being made (especially with software), and to give them mean‐ ingful, well-written commit messages.

The timing for creating commits is up to you, but it's a good practice to commit whenever you've completed a logical chunk of work. For example, if you've implemented a new feature, tested it, and everything works, that's an ideal time to commit. Remember, it's usually better to have smaller, focused commits rather than massive ones that try to cram in many unrelated changes.
{% endhint %}

###

<figure><img src="../../.gitbook/assets/image (7) (1) (1).png" alt=""><figcaption></figcaption></figure>
