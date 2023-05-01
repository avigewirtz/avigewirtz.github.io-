# Notable Directories

The filesystem has many notable directories you need to be familiar with to become a proficient Linux user. We've already covered the root directory. We will now focus on other notable directories.

<figure><img src="https://lh4.googleusercontent.com/BheXyNU0t154mGoTPcX5POBMs60EjSzSdkn4LJezjzPwmA2I4ABbsnOBp3Errnc2t11JstAjl_JbDticzMOhV42yBJ5OMRF5ZyogG0grk_UKCEIFQ_M3rw1P0LazjLliGXaC6lr9QKD2yRIkupm5j50" alt=""><figcaption></figcaption></figure>

### Home directory

Each user on a Linux system is assigned a personal directory, called a _home directory_, for them to store their files and directories. The name of the home directory usually corresponds to the user's login name. On armlab, it corresponds to your NetID.

By default, the contents of a user's home are accessible by the user and the system administrator only, ensuring the privacy and security of the user's files.

Upon login, a user’s home directory is by default their working directory.

### Working directory

Each [process](../../appendices/operating-systems/process.md) has a dynamically associated directory, called a _working directory_**,** which, informally, can be thought of as the "location" where the process is currently "working in." (If this idea seems abstract, it should become more concrete when we cover [pathnames](pathnames.md).)

When you log into a terminal session, your home directory is by default set as your working directory. You can change the working directory, however (using the [`cd` command](../../bash/navigating-the-filesystem/cd-change-working-directory.md), which we'll cover later).

### Hidden files/directories

A file or directory whose name begins with a `.` (period) is called _hidden_. Hidden files/directories are (by default) not visible in directory listings—neither as icons in a GUI nor as text in a CLI. To make hidden entries visible, you must make an explicit request.

### The . (dot) and .. (dot dot) directories

Every directory has at least two hidden directory entries in it: `.` (dot) and `..` (dot dot). The former references the directory itself (i.e., the working directory), and the latter references the parent directory (i.e., the parent of the working directory). These entries serve an important role in [pathnames](pathnames.md).

### Important standard directories

Every Linux filesystem has a set of important directories residing in the root directory. These directories are essential for the proper functioning of a Linux system, and the presence of most of them is required by the [Filesystem Hierarchy Standard](https://refspecs.linuxfoundation.org/FHS\_3.0/fhs/index.html) (FHS). Here is a very brief overview the directories on armlab:

1. _/bin_: Essential binary files, including common commands like `cp`, `mv`, `rm`, and `ls`.
2. _/boot_: Files required for booting, including the kernel, bootloader, and configuration files.
3. _/dev_: Device files that represent hardware devices like hard drives, USB drives, and network devices.
4. _/etc_: System configuration files, including user accounts, system-wide settings, and startup scripts.
5. _/home_: User home directories, where users store personal files and configurations. Note that on armlab, most users home directories are instead stored in a directory names _/u_.&#x20;
6. /lib: Shared library files required by the system and applications.
7. _/lib64_: Contains shared library files that are required by the system and applications for 64-bit architectures
8. _/lost+found_: Used to store files that are recovered during a file system check.
9. /media: Automatically mounts removable media like USB drives or CDs.
10. _/mnt_: Temporarily mounts file systems.
11. _/opt_: Installs optional software packages.
12. _/proc_: Contains system information such as running processes, memory usage, and CPU information.
13. _/root_: Home directory of the root user.
14. _/run_: Rruntime files such as PID files, socket files, and lock files.
15. _/sbin_: System binaries for system administration tasks.&#x20;
16. _/srv_: Used for data served by the system, like website content or FTP files.
17. _/sys_: Iinformation about the system's hardware devices and drivers.
18. _/tmp_: Used for temporary files created by the system and applications.
19. _/usr_: Files not required for booting but required for normal system operation, including application binaries, libraries, and documentation.
20. _/var_: Variable data such as log files, system databases, and spool files.

{% hint style="info" %}
Note that some of these directories are not listed in the above snapshot of the armlab filesystem due to space constraints.
{% endhint %}

