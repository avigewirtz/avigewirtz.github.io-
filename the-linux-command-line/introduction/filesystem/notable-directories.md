# Notable Directories

The filesystem has many notable directories you need to be familiar with to effectively utilize the command line.&#x20;



## Home Directory

Each user on a Linux system is assigned a personal directory, called a _home directory_, for them to store their files and directories. The name of a user's home directory is usually their login name. On Armlab, the name of your home directory is your NetID.

By default, the contents of a user's home are accessible by the user and the system administrator only, ensuring the privacy and security of the user's files.

## Working Directory

Whenever you're using the command line, Bash is always positioned somewhere in the filesystem. This location is known as your (or, more accurately, Bash's) _working directory_. By default, your working directory will be your home directory. You can change the working directory using the `cd` command, which will be covered in [Navigating the Filesystem](../../navigating-the-filesystem/).

The concept of a working directory is at its core a connivence thing, created to enable relative pathnames.&#x20;

{% hint style="info" %}
In fact, every process (running program) always has a dynamically associated directory, called a _working directory_**,** which, informally, can be thought of as the "location" that the process is currently "working in." (If this idea seems abstract, it should become more concrete when we cover [pathnames](pathnames.md).)
{% endhint %}

## Hidden files/directories

Files or directories whose names begin with a  `.` (period) are _hidden_, meaning that by default they are not displayed in directory listings, whether in a GUI or CLI environment. To view these hidden entries, you need to explicitly request for them to be displayed.

## The . (dot) and .. (dot dot) directories

By convention, every directory contains at least two hidden directories: `.` (dot), which refers to the directory itself, and `..` (dot dot), which refers to the parent directory. Being familiar with this notation is critical to using relative pathnames.&#x20;

## Important standard directories

Every Linux filesystem has a set of important directories residing in the root directory. These directories are essential for the proper functioning of a Linux system, and the presence of most of them is required by the [Filesystem Hierarchy Standard](https://refspecs.linuxfoundation.org/FHS\_3.0/fhs/index.html) (FHS). Here is a very brief overview of the directories on armlab:

* _/bin_: Essential binary files, including common commands like `cp`, `mv`, `rm`, and `ls`.
* _/boot_: Files required for booting, including the kernel, bootloader, and configuration files.
* _/dev_: Device files that represent hardware devices like hard drives, USB drives, and network devices.
* _/etc_: System configuration files, including user accounts, system-wide settings, and startup scripts.
* _/home_: User home directories, where users store personal files and configurations. Note that on armlab, most users home directories are instead stored in a directory names _/u_.
* /lib: Shared library files required by the system and applications.
* _/lib64_: Contains shared library files that are required by the system and applications for 64-bit architectures
* _/lost+found_: Used to store files that are recovered during a file system check.
* /media: Automatically mounts removable media like USB drives or CDs.
* _/mnt_: Temporarily mounts file systems.
* _/opt_: Installs optional software packages.
* _/proc_: Contains system information such as running processes, memory usage, and CPU information.
* _/root_: Home directory of the root user.
* _/run_: Rruntime files such as PID files, socket files, and lock files.
* _/sbin_: System binaries for system administration tasks.
* _/srv_: Used for data served by the system, like website content or FTP files.
* _/sys_: Information about the system's hardware devices and drivers.
* _/tmp_: Used for temporary files created by the system and applications.
* _/usr_: Files not required for booting but required for normal system operation, including application binaries, libraries, and documentation.
* _/var_: Variable data such as log files, system databases, and spool files.

{% hint style="warning" %}
Note that some of these directories are not listed in the above snapshot of the armlab filesystem due to space constraints.
{% endhint %}
