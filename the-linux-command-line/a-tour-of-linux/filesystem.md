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

The Linux filesystem is organized as a single hierarchical structure, resembling an inverted tree. At the base is the _root directory_, denoted `/` (slash), from which all files and directories in the system descend. A partial snapshot of the Armlab directory hierarchy is shown in Figure 1.

<figure><img src="../../.gitbook/assets/filesystem10.17 (16).png" alt=""><figcaption><p>Partial snapshot of Armlab directory hierarchy</p></figcaption></figure>

{% hint style="info" %}
The terms _parent_ and _child_ are commonly used to describe the relationship between a two adjacent directories. In the above snapshot, for example, `tal5` is a child of `u` (and `u` is the parent of `tal5`, `bwk`, and `sgewirtz`).
{% endhint %}



### Home Directory

Each user on a Linux system has a personal directory called a _home directory_. This is a designated space to store personal files and directories. On Armlab, your home directory is located in the `/u` directory and is named after your NetID (Figure 15). For example, if your NetID is "tal5", your home directory would be `/u/tal5`. By default, the contents of your home directory are not accessible to other users (with the exception of the system administrator).

<figure><img src="../../.gitbook/assets/filesystem10.17 (15).png" alt=""><figcaption><p>Figure 15: Home directories</p></figcaption></figure>

### Pathnames

* Imagine a company where all files are stored within a single, main filing cabinet. This cabinet represents the root folder. Inside, there are folders for shared company documents, like "Financial Reports" or "Marketing Materials." Additionally, each employee has their personal folder within the main cabinet. each employee does not have permission to look in another employees folder. only shared folders and their own.
* Suppose many assistant whos job it is to retrieve files for employees. How does each employee request a file from one of the assistants? For example, say an assistant wanted a file named Q2\_Financial\_Report.xlsx. How do they instruct the assistant?&#x20;
* Giving the assistant instructions like "please get me Q2\_Financial\_Report.xlsx" would be a pretty bad idea. First, the assistant would have no idea where this file is located. granted, they wouldn't have to search the entire system. But they don't know where in the shared files or employees personal personal folder it is. having them search every folder would be a huge waste of time. Second, Even if the assistant could search every folder, what if there's more than one file named "Q2\_Financial\_Report.xlsx?" the assistant wouldn't know which the employee wanted. Sure, they could ask each time they see a file named Q2\_Financial\_Report.xlsx, but this would be super annoying. and what if the employee is out on lunch break?
* To make everyone's life easier, could provide explicit instructions, like the following:&#x20;
* Please start at the main file cabinet, then go to the 'employees folder,' then go to my personal folder, then go to financials folder, open the 'Accounting' folder (another subdirectory), and you'll find the 'Q2\_Financial\_Report.xlsx' file inside." Assuming you don't keep any two files with the same name in the same folder, this scheme works. This provides a complete roadmap from the starting point to the exact file location.&#x20;
* However, if I frequently request files, repeating these types of directions every time gets cumbersome for me to repeat. just a long sentence. takes too much time. Instead, we devise a simple solution. Unless each employee explicitly tells the assistant to start at the main folder, it's implicitly assumed they they start at the employees personal directory. This makes sense since most of the time the employee needs to specify a file in their personal folder. Now, when the employee asks for "2\_Financial\_Report.xlsx" an employee asks
* Let's say we establish the "Accounting" folder as our default starting point. Now, I can simply say, "please go to financials folder, open the 'Accounting' folder (another subdirectory), and you'll find the 'Q2\_Financial\_Report.xlsx".&#x20;
* Furthermore, at any point, the employee can change the default starting point, individually for each employee. For example, employee can tell one assistant "for the rest of the day,  "Accounting" folder is our default starting point. Now, all i have to say is "please retrieve Q2\_Financial\_Report.xlsx", and assitant know where to find it. can give another assitant a different default starting point.&#x20;
* Tie it in to absolute and relative pathnames in Linux filesystems. Employees are like each user on computer. Assitants are like processes (running program). by default, Assistant
*
* You'll understand to start your search within the "Accounting" folder. At any point, I can change the default starting point. so let's say

We can pinpoint the location of any file in the directory hierarchy by specifying its&#x20;



Suppose we want to open a file, such as `the_odyssey.txt`, with a text editor like Emacs. How to we do so? Giving Emacs a command like "open the\_odyssey.txt" would not work, for two reasons. First, Emacs does not know where `the_odyssey.txt` is located in the filesystem. While it could theoretically search the entire filesystem, this would be prohibitively time-consuming, given how large modern filesystems are. Second, what if there's more than one file named `the_odyssey.txt`. How would Emacs know which one to open?&#x20;

As you probably guessed, we have to give Emacs "directions" on where to find where to find the\_oddysey.txt. This can be done is by specifying the path from the root directory. The directions would go something like this: "Start from the root directory, go to u, then sgewirtz, then CLI\_playground, and there you'll find the\_odyssey.txt. In Linux syntax, we'd express such a path as follows: `/u/sgewirtz/CLI_playground/the_odyssey.txt`. This is known as an absolute pathname.&#x20;

We'd type&#x20;

Typing out long pathnames is annoying, however. Imagine if every time you wanted to open the\_oddysey.txt, you'd have to invoke:

```
emacs /u/sgewirtz/CLI_playground/the_odyssey.txt
```

For this reason, each process (running program), has&#x20;
