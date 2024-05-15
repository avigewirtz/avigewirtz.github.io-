# The Filesystem

One of the core services of the Linux kernel is the provision of a filesystem, which is an abstracted model of computer storage. Here, we discuss the basics of the Linux filesystem.&#x20;

### Files

At its core, a file is a linear array of bytes of arbitrary length. Each file has a _type_ that indicates its role:

* A _regular file_ contains arbitrary data, such as text, images, audio, executable programs, and so on. Essentially, just about any kind of data you can think of can be stored in a regular file.
* A _directory_ is a file that holds a structured list of links. Each link maps a filename to a file, which may itself be a directory. Every directory contains at least two entries: `.` (dot), which is a link to itself, and `..` (dotdot), which is a link to its parent. The fact that directories can contain subdirectories enables a hierarchical filesystem structure, as we'll see shortly.

{% hint style="info" %}
Other types of files include named pipes, sockets, symbolic links, and character and block device files, which are beyond our scope.
{% endhint %}

{% hint style="info" %}
**Note on terminology**

I use the term "files" generally to refer to both regular files and directories. I will specify the type only when the distinction is necessary.
{% endhint %}

### Filenames

Linux places very few restrictions on filenames. Filenames may not contain the `/` or ASCII NUL character, and no two files in the same directory may have the same name. Note, however, that filenames are case-sensitive; that is, `hello.c`, `Hello.c`, and `HELLO.C` refer to three distinct files, and all may exist in the same directory.

{% hint style="info" %}
#### Filename Extensions

Linux itself has no concept of filename extensions. It treats them as ordinary characters in a filename. Some programs, however, require filename extensions. For example, GCC won't compile a file unless it has an extension like `.c`_._ To be clear, however, this is a feature of GCC, not Linux.&#x20;
{% endhint %}

#### Hidden Files

Files whose names begin with a `.` (e.g., `.bashrc`) are _hidden_, meaning that by default, they are not displayed in directory listings—whether in a GUI or CLI environment. We will cover how to display them in our discussion of the `ls` command.

### Single Directory Hierarchy

The Linux filesystem is organized as a single hierarchical structure, resembling an inverted tree. At the base is the _root directory_, denoted `/` (slash), from which all files and directories in the system descend. A partial snapshot of the Armlab directory hierarchy is shown in Figure 1.

<figure><img src="../../.gitbook/assets/filesystem10.17 (16).png" alt=""><figcaption><p>Partial snapshot of Armlab directory hierarchy</p></figcaption></figure>

{% hint style="info" %}
The terms _parent_ and _child_ are commonly used to describe the relationship between two adjacent directories. In the above snapshot, for example, `tal5` is a child of `u` (and `u` is the parent of `tal5`, `bwk`, and `sgewirtz`).
{% endhint %}

### Home Directory

Each user on a Linux system has a personal directory called a _home directory_. This is a designated space to store personal files and directories. On Armlab, your home directory is located in the `/u` directory and is named after your NetID. For example, if your NetID is "tal5", your home directory would be `/u/tal5` (Figure 15). By default, the contents of your home directory are not accessible to other users (with the exception of the system administrator).

<figure><img src="../../.gitbook/assets/filesystem10.17 (15).png" alt=""><figcaption><p>Figure 15: Home directories</p></figcaption></figure>

### Working Directory

Whenever you're using the command line, the shell (e.g., Bash) is always positioned somewhere in the filesystem. This location is known as your (or, more accurately, the shell's) _working directory_. By default, your working directory will be your home directory, but you can change it using the `cd` command (covered in [Navigating the Filesystem](../navigating-the-filesystem/#cd-relocating)).

{% hint style="info" %}
Every running program on your computer--not just the shell--has a working directory. When you launch a program (e.g., `ls`, `gcc`, `emacs`, `cat`) with the shell, that program inherits the shell's working directory and uses it to resolve relative pathnames (see below).&#x20;
{% endhint %}

### Pathnames

Every file has a _pathname_, which is a string that identifies its location in the directory hierarchy. Pathnames come in two forms:

* An _absolute pathname_ pinpoints the location of a file by specifying its path from the root directory. It starts with a forward slash (/) followed by zero or more filenames, each separated by slashes. For example, in Figure 16, the absolute pathname of `the_odyssey.txt` is `/u/sgewirtz/CLI_playground/the_odyssey.txt`. Absolute pathnames are unambiguous because they don't depend on the current working directory.
* A _relative pathnames_ pinpoints the location of a file or directory by specifying its path from the working directory. It consists of zero or more filenames, each separated by slashes. For example, in Figure 15, if `/u/sgewirtz` is the current working directory, then the relative pathname for `the_odyssey.txt` is `./CLI_playground/the_odyssey.txt`. If `/u/sgewirtz/CLI_playground` is the current working directory, however, then the relative pathname is `./the_odyssey.txt`.
