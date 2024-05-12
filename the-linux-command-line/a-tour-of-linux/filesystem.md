# The Filesystem

One of the core services of the Linux kernel is the Provision of a file system filesystem, which is an abstraction of computer storage. Here, we discuss the basics of the Linux filesystem.&#x20;

### Files

At its core, a file is a linear array of bytes of arbitrary length. Each Linux file has a _type_ that indicates its role:

* A _regular file_ contains arbitrary data, such as text, images, audio, executable programs, and so on. Essentially, just about any kind of data you can think of can be stored in a regular file.
* A _directory_ is a file that holds a structured list of links. Each link maps a filename to a file, which may itself be a directory. Every directory contains at least two entries: `.` (dot), which is a link to itself, and `..` (dotdot), which is a link to its parent.

{% hint style="info" %}
Other types of files include named pipes, sockets, symbolic links, and character and block device files, which are beyond our scope.
{% endhint %}

### Filenames

Linux places very few restrictions on filenames. Filenames may not contain the `/` or ASCII NUL character. Additionally, no two files in the same directory may have the same name. Note, however, that filenames are case-sensitive; that is, `hello.c`, `Hello.c`, and `HELLO.C` refer to three distinct files, and all may exist in the same directory.

#### Filename Extensions

Linux itself has no concept of filename extensions. It treats them as ordinary characters in a filename. Some programs, however, require filename extensions. For example, Microsoft Word won't open a file unless it has an extension like `docx`_._&#x20;

#### Hidden Files

Files whose names begin with a `.` (e.g., `.bashrc`) are _hidden_, meaning that by default, they are not displayed in directory listings—whether in a GUI or CLI environment. We will cover how to display them in our discussion of the `ls` command.

### Single Directory Hierarchy

The Linux filesystem is organized as a single hierarchical structure, resembling an inverted tree. At the base is the _root directory_, denoted by `/` (slash), from which all files and directories in the system descend. A partial snapshot of the Armlab filesystem is shown in Figure 1.

<figure><img src="../../.gitbook/assets/filesystem10.17 (16).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
The terms _parent_ and _child_ are commonly used to describe the relationship between a two adjacent directories. In the above snapshot, for example, `tal5` is a child of `u` (and `u` is the parent of `tal5`, `bwk`, and `sgewirtz`).
{% endhint %}

### Pathnames

Suppose we want to open a file, such as `the_odyssey.txt`, with a text editor like Emacs. How to we do so? Giving Emacs a command like "open the\_odyssey.txt" would not work, for two reasons. First, Emacs does not know where `the_odyssey.txt` is located in the filesystem. While it could theoretically search the entire filesystem, this would be prohibitively time-consuming, given how large modern filesystems are. Second, what if there's more than one file named `the_odyssey.txt`. How would Emacs know which one to open?&#x20;

As you probably guessed, we have to give Emacs "directions" on where to find where to find the\_oddysey.txt. This can be done is by specifying the path from the root directory. The directions would go something like this: "Start from the root directory, go to u, then sgewirtz, then CLI\_playground, and there you'll find the\_odyssey.txt. we'd express this as follows: `/u/sgewirtz/CLI_playground/the_odyssey.txt`. This is known as an absolute pathname.&#x20;

Typing out long pathnames is annoying, however. Imagine if every time you wanted to open the\_oddysey.txt, you'd have to invoke:

```
emacs /u/sgewirtz/CLI_playground/the_odyssey.txt
```

For this reason, each process (running program), including emacs of course, has&#x20;

### Home Directory

Each user on a Linux system has a personal directory called a _home directory_. This is a designated space to store personal files and directories. On Armlab, your home directory is located in the `/u` directory and is named after your NetID (Figure 15). For example, if your NetID is "tal5", your home directory would be `/u/tal5`. By default, the contents of your home directory are not accessible to other users (with the exception of the system administrator).

<figure><img src="../../.gitbook/assets/filesystem10.17 (15).png" alt=""><figcaption><p>Figure 15: Home directories</p></figcaption></figure>

### Working Directory

Each process (instance of a running program) has a dynamically associated directory, called its _working directory_**,** which is the location the process is currently "working in." By default, your working directory will be your home directory, but you can change it using the `cd` command, which we'll cover in in [Navigating the Filesystem](../navigating-the-filesystem/#cd-relocating).

### Pathnames

Every file has a _pathname_, which is a string that identifies its location in the directory hierarchy. Pathnames come in two forms:

* An _absolute pathname_ pinpoints the location of a file by specifying its path from the root directory. It starts with a forward slash (/) followed by zero or more filenames, each separated by slashes. For example, in Figure 16, the absolute pathname of `the_odyssey.txt` is `/u/sgewirtz/CLI_playground/the_odyssey.txt`. Absolute pathnames are unambiguous because they don't depend on the current working directory.
* A _relative pathnames_ pinpoints the location of a file or directory by specifying its path from the working directory. It consists of zero or more filenames, each separated by slashes. For example, in Figure 15, if `/u/sgewirtz` is the current working directory, then the relative pathname for `the_odyssey.txt` is `./CLI_playground/the_odyssey.txt`. If `/u/sgewirtz/CLI_playground` is the current working directory, however, then the relative pathname is `./the_odyssey.txt`.
