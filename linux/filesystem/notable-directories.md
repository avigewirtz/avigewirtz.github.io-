# Notable Directories

The filesystem has many notable directories. We've already covered the root directory. We will now focus on other notable directories.

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

These directories reside in the root directory and are crucial for the proper functioning of the Linux system. They are typically accessible to the system administrator only. If you are curious about their function, here is a very brief explanation of each:

* `/bin`: essential binary executables
* `/boot`: files needed to boot the system
* `/dev`: device files for hardware interaction
* `/etc`: configuration files and directories
* `/sbin`: system binary executables for administration
* `/lib`: shared libraries for binaries
* `/lost+found`: recovered files
* `/root`: home directory for the root user
* `/u`: home directories for individual users
* `/usr`: user-installed applications and resources
* `/var`: variable data, such as log files and databases

Note that this is only a partial list and that the precise names of the directories can vary by Linux distribution or computer.
