# Setting up a git project

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

To stage all changes in the working tree, invoke:

```
git add -A
```

If you're in the root directory of your project, then these two commands are functionally equivalent.&#x20;

### Committing

The general form of a Git commit command is as follows:

```bash
git commit -m "COMMIT_MESSAGE"
```

Where COMMIT\_MESSAGE is replaced with a concise, meaningful description of the changes you made. This message becomes a part of your commit and helps you (and potentially others) understand the purpose of the commit when reviewing the project's history. In our case, since it's our first commit and we don't have anything meaningful to say, we'll simply write "first commit" in the message spot:

<figure><img src="../../.gitbook/assets/Screenshot 2024-04-04 at 4.47.23 PM.png" alt="" width="563"><figcaption></figcaption></figure>

The result is that a snapshot of the current state of our project is now stored in the repository. For simplicity, we label this commit "commit 1," but as we'll see soon, commits are identified by a 40-digit hex number.&#x20;

<figure><img src="../../.gitbook/assets/Group 131.png" alt="" width="375"><figcaption><p>Figure 3: Our repository after the first commit.</p></figcaption></figure>
