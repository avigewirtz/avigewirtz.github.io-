# Linux Filesystem

### Files

At its core, a file is a linear array of bytes of arbitrary length. Each Linux file has a _type_ that indicates its role:

* A _regular file_ contains arbitrary data, such as text, images, audio, executable programs, and so on. Linux does not distinguish between different types of files.&#x20;
* A _directory_ is a file that contains an array of links, where each entry maps a filename to a file, which may be another directory.&#x20;

{% hint style="info" %}
Other types of files include named pipes, sockets, symbolic links, and character and block device files, which are beyond our scope.&#x20;
{% endhint %}

### Filenames

A few notes filenames in Linux are worthy of mention:

* Linux places very few restrictions on filenames. No two filenames in the same directory may be the same, and filenames may not contain the  `/` and _ASCII NUL_ characters_._&#x20;
* Filenames are case-sensitive; that is, _hello.c_, _Hello.c_ and _HELLO.C_ refer to three distinct files.&#x20;
* Linux has no concept of filename extension. They are entirely optional and treated as ordinary filename characters. In other words,&#x20;
* Files whose names begin with a  `.`  (e.g., `.bashrc`) are _hidden_, meaning that by default they are not displayed in directory listings--whether in a GUI or CLI environment. We'll go over how to display them in our coverage of the [`ls`](../navigating-the-filesystem/#ls-a-sense-of-surroundings) command.&#x20;

### Single Directory Hierarchy

The Linux filesystem is organized as a single hierarchical structure, resembling an inverted tree. At the base is the _root directory_, denoted by `/` (slash), from which all files and directories in the system descend. An example of this hierarchical structure is shown in Figure 1, which depicts a partial snapshot of the Armlab filesystem.

<figure><img src="../../.gitbook/assets/filesystem10.17 (16).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
The terms _parent_ and _child_ are commonly used to describe the relationship between a two adjacent directories. In the above snapshot, for example, `tal5` is a child of `u` (and `u` is the parent of `tal5`, `bwk`, and `sgewirtz`).
{% endhint %}

## Home Directory

Each user on a Linux system has a personal directory called a _home directory_. This is a designated space to store personal files and directories. On Armlab, your home directory is located in the `/u` directory and is named after your NetID (Figure 15). For example, if your NetID is "tal5", your home directory would be `/u/tal5`. By default, the contents of your home directory are not accessible to other users (with the exception of the system administrator).

<figure><img src="../../.gitbook/assets/filesystem10.17 (15).png" alt=""><figcaption><p>Figure 15: Home directories</p></figcaption></figure>

### Working Directory

Each process (instance of a running program) has a dynamically associated directory, called its _working directory_**,** which, informally, can be thought of as the location where the process is currently "working in." By default, your working directory will be your home directory, but you can change it using the `cd` command, which is covered in [Navigating the Filesystem](../navigating-the-filesystem/#cd-relocating).

### The `.` (dot) and `..` (dot dot) Directory Entries

Every directory contains at least two entries: `.` (dot), which is a link to itself, and `..` (dot dot), which is a link to its parent.&#x20;

### Pathnames

Every file has a _pathname_, which is a string that identifies its location in the directory hierarchy. Pathnames come in two forms:

* An _absolute pathname_ pinpoints the location of a file by specifying its path from the root directory. It starts with a forward slash (/) followed by zero or more file names, each separated by slashes. For example, in Figure 15, the absolute pathname of `the_odyssey.txt` is `/u/sgewirtz/CLI_playground/the_odyssey.txt`. Absolute pathnames are unambiguous because they don't depend on the current working directory.
* A _relative pathnames_ pinpoints the location of a file or directory by specifying its path from the working directory. It consists of zero or more file names, each separated by slashes. For example, in Figure 15, if `/u/sgewirtz` is the current working directory, then the relative pathname for "the\_odyssey.txt" is `./CLI_playground/the_odyssey.txt`. If `/u/sgewirtz/CLI_playground` is the current working directory, then the relative pathname is simply `./the_odyssey.txt`.
