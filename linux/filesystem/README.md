# Filesystem

One of the most fundamental features of the operating system is the filesystem. From the user's point of view, the filesystem consists of two main components: (1) a collection of files, and (2) a directory structure that organizes these files. Before delving into the details of the Linux filesystem, we'll first provide a brief overview of Linux files and directories.

{% hint style="warning" %}
The term "Linux filesystem" is a bit of a misnomer, as Linux does not have any official filesystems or even an authoritative filesystem standard. Rather, the term refers to a variety of filesystems that are supported by the Linux kernel and share a common set of features inherited from Unix.

Of the many Linux-supported filesystems, some of these filesystems were specifically developed for Linux, while others were initially created for other operating systems but have since been adapted to work with Linux. This flexibility allows users to choose the filesystem that best suits their needs and preferences.

Commonly used filesystems supported by Linux include Ext4 (used on armlab), XFS, Btrfs, FAT32, and NTFS.
{% endhint %}
