# Files

Linux organizes all data in computer storage into files. At its core, a file is a linear array of bytes of arbitrary length. Each Linux file has a _type_ that indicates its role:

* A _regular file_ contains arbitrary data. Application program's typically distinguish between text files, which are regular files that contain only ASCII or Unicode characters, and binary files, which contain everything else.&#x20;
* A _directory_ is a file that contains an array of links, where each entry maps a filename to a file, which may be another directory.  Every directory contains a link to itself and to its parent directory. The `.` (dot) and `..` (dot dot) directory entries.&#x20;

Other types of files include named pipes, sockets, symbolic links, and character and block device files, which are beyond our scope.&#x20;

{% hint style="info" %}
The folder metaphor is often used&#x20;
{% endhint %}

### Filenames

Every file has a _filename_. On Linux, filenames are case-sensitive; that is, _hello.c_, _Hello.c_ and _HELLO.C_ refer to three distinct files.

Very few restrictions are placed on filenames.&#x20;

* No two filenames in the same directory may be the same.
* Filenames may not exceed 255 bytes. (This normally corresponds to 255 characters.)
* Filenames may not contain a `/`, which is reserved for separating directory paths, or the _ASCII NUL_ character.&#x20;

While any filename adhering to these rules is considered valid, some filenames are not ideal for use in a shell environment and are best avoided, as will be discussed [later](../../basic-file-and-directory-operations/creating-files-and-directories.md#directory-and-file-creation).

### Hidden files/directories

Files whose names begin with a  `.` (period) are _hidden_, meaning that by default they are not displayed in directory listings--whether in a GUI or CLI environment. We'll go over how to display them when we cover the [`ls`](../../navigating-the-filesystem/#ls-a-sense-of-surroundings) command.&#x20;



{% hint style="info" %}
### Filename Extensions

Linux has no concept a of filename extension. Meaning, it does not A filename extension is a suffix added to the end of a filename, beginning with a dot, that usually indicates the format or type of the file. The extension is usually composed of three or four letters, but it can also be longer.

Filename extensions are not an inherent feature of Linux filesystems; thus, from Linux's perspective, they are entirely optional and treated as ordinary filename characters. However, some programs require input files to have filename extensions, as they depend on them to determine the file type or enforce specific conventions. For instance, the GCC compiler will not compile a C program unless it has a _.c_ or _.i_ extension.

Even when not required, using filename extensions is considered good practice, as it helps users and software more easily identify the contents of a file.
{% endhint %}
