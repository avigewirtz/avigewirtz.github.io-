# Linux Filesystem

One of the most fundamental services provided by the operating system is the filesystem, which is an abstracted model of computer storage. Filesystem contains a collection of files organized into directories. At its core, a file is a linear array of bytes of arbitrary length. Each Linux file has a _type_ that indicates its role:

* A _regular file_ contains arbitrary data, such as text, images, audio, executable programs, and so on. Application program's typically distinguish between different types of files, but Linux. To the kernel there is no difference between text and binary files.
* A _directory_ is a file that contains an array of links, where each entry maps a filename to a file, which may be another directory. Every directory contains at least two entries: `.` (dot), which is a link to itself, and `..` (dot dot), which is a link to its parent.&#x20;

{% hint style="info" %}
Other types of files include named pipes, sockets, symbolic links, and character and block device files, which are beyond our scope.&#x20;
{% endhint %}

## Directory Hierarchy

The Linux filesystem is organized as a single hierarchical structure, resembling an inverted tree. At the base is the _root directory_, denoted by `/` (slash), from which all files and directories in the system descend. An example of this hierarchical structure is shown in Figure 1, which depicts a partial snapshot of the Armlab filesystem.

<figure><img src="../../../.gitbook/assets/filesystem10.17 (16).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
The terms _parent_ and _child_ are commonly used to describe the relationship between a adjacent directories. In the above snapshot, for example, `tal5` is a child of `u` (and `u` is the parent of `tal5`, `bwk`, and `sgewirtz`).
{% endhint %}

#### Filenames

A few notes filenames in Linux are worthy of mention:

* Linux places very few restrictions on filenames. No two filenames in the same directory may be the same, and filenames may not contain the  `/` and _ASCII NUL_ characters_._&#x20;
* Filenames are case-sensitive; that is, _hello.c_, _Hello.c_ and _HELLO.C_ refer to three distinct files.&#x20;
* Linux has no concept of filename extension. They are entirely optional and treated as ordinary filename characters. In other words,&#x20;
* Files whose names begin with a  `.`  (e.g., `.bashrc`) are _hidden_, meaning that by default they are not displayed in directory listings--whether in a GUI or CLI environment. We'll go over how to display them in our coverage of the [`ls`](../../navigating-the-filesystem/#ls-a-sense-of-surroundings) command.&#x20;

{% hint style="info" %}
To avoid having to always say "files and directories", will often refer to them as just files. This is techincally correct, since directory is a type of file. When there is a clear distinction
{% endhint %}

{% hint style="info" %}
Important standard directories

Every Linux filesystem has a set of important directories residing in the root directory. These directories are essential for the proper functioning of the system, and the presence of most of them is required by the [Filesystem Hierarchy Standard](https://refspecs.linuxfoundation.org/FHS\_3.0/fhs/index.html) (FHS). Here is a very brief overview of many of these directories:&#x20;
{% endhint %}

## Home Directory

Each user on a Linux system has a personal directory called a _home directory_. This is a designated space to store personal files and directories. On Armlab, your home directory is located in the `/u` directory and is named after your NetID. For example, if your NetID is "tal5", your home directory would be `/u/tal5` (Figure 15). By default, the contents of your home directory are not accessible to other users (with the exception of the system administrator).

<figure><img src="../../../.gitbook/assets/filesystem10.17 (15).png" alt=""><figcaption><p>Figure 15: Home directories</p></figcaption></figure>

