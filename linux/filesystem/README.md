# Filesystem

One of the fundamental features of an operating system is the _filesystem. A_ filesystem consists of two parts: (1) a collection of files; and (2) a directory structure that organizes the files. Before getting into the details of the Linux filesystem, it makes sense to first give an overview of Linux files and directories.

{% hint style="info" %}
The term "Linux filesystem" is a bit of a misnomer, as Linux does not have any official filesystems or even an official filesystem standard. Rather, the term refers to a variety of filesystems that are supported by the Linux kernel and share a common set of features inherited from Unix.&#x20;

Of the many Linux-supported filesystems, some of these filesystems were specifically designed for Linux, while others were initially created for different operating systems but have since been adapted to work with Linux. This flexibility allows users to choose the filesystem that best suits their needs and preferences.

Some of the commonly used filesystems supported by Linux include Ext4 (used by armlab), XFS, Btrfs, FAT32, and NTFS.&#x20;
{% endhint %}
