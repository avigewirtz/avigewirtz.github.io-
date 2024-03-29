# Files and Directories

### Files

At its core, a Linux file is simply a sequence of bytes. When these bytes are structured in a meaningful way, they are interpretable by programs and able to be rendered by them as text, photos, videos, music, executable programs, and so on. A file is the smallest unit of computer storage; everything in storage is contained in a file.

Linux does not require files to have any particular internal structure. As far as Linux is concerned, a file may be composed of any arbitrary sequence of bytes. However, many programs impose their own set of formatting rules that files must conform to in order for the files to be executed by them. For example, Microsoft Word will not open a file unless its internal structure meets a format such as _doc_. Similarly, Linux will not execute a file unless it is formatted with specific sections. (You will learn about this later in COS217.) In general, encoding schemes and formatting rules transform files from meaningless sequences of bytes into comprehensible units of information.

### Directory

A directory is a unique type of file—one that contains references to other files (and directories). Grouping related files into directories keeps the filesystem organized, making it easier to locate files.

{% hint style="info" %}
On Windows, directories are called _folders_.
{% endhint %}
