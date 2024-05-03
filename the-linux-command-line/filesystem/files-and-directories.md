# Files and Directories

### Files

At its core, a file in Linux is a storage container that contains nothing more than a sequence of bytes. When these bytes are structured in a meaningful way, they are interpretable by programs and able to be rendered by them as text, photos, videos, music, executable programs, and so on. A file is the smallest unit of computer storage; everything in storage is contained in a file.

Linux does not require files to have any particular internal structure. As far as Linux is concerned, a file may be composed of any arbitrary sequence of bytes. However, many programs impose their own set of formatting rules that files must conform to in order for the files to be executed by them. For example, Microsoft Word will not open a file unless its internal structure meets a format such as _doc_. Similarly, Linux will not execute a file unless it is formatted with specific sections. (You will learn about this later in COS217.) In general, encoding schemes and formatting rules transform files from meaningless sequences of bytes into comprehensible units of information.

### Directory

A directory is a unique type of file—one that contains references to other files (and directories). Grouping related files into directories keeps the filesystem organized, making it easier to locate files.

{% hint style="info" %}
On Windows, directories are called _folders_.
{% endhint %}

## Filenames

Every file has a _filename_. On Linux, filenames are case-sensitive; that is, _hello.c_, _Hello.c_ and _HELLO.C_ refer to three distinct files.

Very few restrictions are placed on filenames. On armlab, which uses the popular Ext4 filesystem, only the following restrictions are imposed:

* No two filenames in the same directory may be the same.
* Filenames may not exceed 255 bytes. (This normally corresponds to 255 characters.)
* Filenames may not contain a _/_ (forward slash), which is reserved for seperating directory paths, or the _ASCII NUL_ character.&#x20;

While any filename adhering to these rules is considered valid, some filenames are not ideal for use in a shell environment and are best avoided, as will be discussed [later](../basic-file-and-directory-operations/creating-files-and-directories.md#directory-and-file-creation).

### Filename extensions

A filename extension is a suffix added to the end of a filename, beginning with a dot, that usually indicates the format or type of the file. The extension is usually composed of three or four letters, but it can also be longer. In the filename _document.txt_, the extension is _.txt_, which indicates that the file is a text file. Other common extensions include _.jpg_ for image files, _.mp3_ for audio files, and _.pdf_ for document files.

Filename extensions are not an inherent feature of Linux filesystems; thus, from Linux's perspective, they are entirely optional and treated as ordinary filename characters. However, some programs require input files to have filename extensions, as they depend on them to determine the file type or enforce specific conventions. For instance, the GCC compiler will not compile a C program unless it has a _.c_ or _.i_ extension.

Even when not required, using filename extensions is considered good practice, as it helps users and software more easily identify the contents of a file.
