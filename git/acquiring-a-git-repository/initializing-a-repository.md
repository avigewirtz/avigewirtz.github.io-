# Initializing a repository

Suppose we have a project named greetings, which consists of the files shown in Figure 3. Two files: hello.txt, which simply contains the word "hello", and hi.txt which contains the word "hi".&#x20;

{% hint style="success" %}
if you want to follow along, simple open a terminal window and invoke the following four commands:

mkdir greetings

cd greetings

echo "hello" > hello.txt

echo "hi" > hi.txt

This will create a directory named greetings and and populate it with hello.txt and hi.txt.&#x20;
{% endhint %}

We want to version control it with git. Initializing a repository is perhaps the simplest task in git. Simply invoke:

```
git init
```

note that init is short for initialize. If we now invoke ls -a, we will see a directory named .git:









This creates a new subdirectory named `.git` that contains all of your necessary repository files — a Git repository skeleton. At this point, nothing in your project is tracked yet. See [Git Internals](https://git-scm.com/book/en/v2/ch00/ch10-git-internals) for more information about exactly what files are contained in the `.git` directory you just created.





#### Current state of our repo



If you want to start version-controlling existing files (as opposed to an empty directory), you should probably begin tracking those files and do an initial commit. You can accomplish that with a few `git add` commands that specify the files you want to track, followed by a `git commit`:

```console
$ git add *.c
$ git add LICENSE
$ git commit -m 'Initial project version'
```

We’ll go over what these commands do in just a minute. At this point, you have a Git repository with tracked files and an initial commit.









