# File and Directory Access Permissions

Linux is a multiuser operating system. In simple terms, that means that a single Linux computer can be shared by many users, all of whom may be logged in simultaneously.&#x20;

{% hint style="info" %}
If the idea of a multiuser computer seems foreign or reminiscent of the Stone Age when computers were as large and expensive as cars and had to be shared by entire organizations, recall that Armlab is shared by hundreds of students and faculty (some of whom might be logged in the same time that you are).
{% endhint %}

### Users

Each user is identified by a unique login name and a corresponding numeric _User ID_ (UID). UIDs are usually assigned by the system administrator, with normal users having UIDs above 500. The system administrator, also known as the superuser or root user, has a UID of 0 and typically uses the username _root_.

User information, including the username, UID, and other details, are stored in the _/etc/passwd_ file. Each line in this file represents a user and contains the following fields separated by colons:

```bash
username:password:UID:GID:comment:home_directory:shell
```

### Groups

In certain situations, it is convenient to treat a set of users as a single entity. For example, we might want to treat all students in a course as a single entity for the purpose of granting access to a common set of files. We do this by associating a list of usernames with a single group. Each group has a unique group name and a corresponding numeric _Group ID_ (GID). A user can belong to multiple groups, and group membership is defined by the system administrator.

Group information is stored in the _/etc/group_ file. Each line in this file represents a group and contains the following fields separated by colons:

```makefile
group_name:password:GID:user_list
```



## Viewing user and group information

You can display your login name, group name, UID, and GID by issuing the `id` command. When I issue it on armlab, I get the following output:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-27 at 11.56.24 PM.png" alt=""><figcaption></figcaption></figure>

Let's break that down:

* `uid=127000(sgewirtz)`: This part of the output shows my User ID (_127000_) and my username (_sgewirtz_).&#x20;
* `gid=35(utempter)`: This part of the output shows my primary Group ID (_35_) and the associated group name (_utemper_).&#x20;
* `groups=35(utempter)`: This part of the output lists all the groups that I belong to, which is only one group (_utemper_).&#x20;
* `context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023`: This part of the output displays the SELinux (Security-Enhanced Linux) context associated with the user. SELinux is a security feature in Linux that enforces access control policies, the details of which are not important for our discussion.&#x20;

\
\








A Linux system like armlab has many users with login accounts. To maintain privacy and security, access rights to each file and directory is strictly regulated.&#x20;

Associated with each file and directory are three categories of users to whom permissions may be granted to:&#x20;

* **Owner**: Typically, the user who created a file is its owner, but ownership can be changed by the superuser.
* **Group**: A predefined group of users.&#x20;
* **Other**:  All other users.

Each of these user categories may be granted three types of permissions: read, write, and execute. The three access permissions are denoted on the command line with three bits: `rwx`,corresponding to read, write, and execute respectively. These permissions have different meanings depending on whether they are applied to files or directories.&#x20;

### File access permissions

For ordinary files, the meanings are pretty self-explanatory:&#x20;

* **Read**: The contents of the file may be read.&#x20;
* **Write**: The contents of the file may be modified.
* **Execute**: The (executable) file may be executed.&#x20;

### Directory access permissions

{% hint style="info" %}
In the context of directory access permissions, it is helpful to recognize that a directory is simply a file with a list of entries (files and other directories that it points to).
{% endhint %}

For directories, the meanings are very confusing. The gist is as follows:

* **Read**: The names of the directory’s entries (i.e., files and subdirectories) may be listed (e.g., by using the ls command). Note that read permission on a directory only lets you view the file and directory names, but not their attributes (i.e., metadata). For that, you must have execute permissions.
* **Write**: Directory entries may be modified (i.e, created, deleted, and renamed and have their attributes modified.). Note that this only applies if the execute permission is also enabled. If execute is not enabled, write permission is totally meaningless.&#x20;
* **Execute**: Directory entries may be accessed, and you may make the directory your working directory. Note that if a directory cannot be accessed, neither can its children, regardless of your permissions for the children themselves. &#x20;

{% hint style="warning" %}
* If you have write and execute permissions on a directory, you can delete its files and empty directories even if you do not have any permission on the files or directories themselves.&#x20;
* To access a file or directory, execute permission is required on all of the directories in the pathname. For example, reading the file /u/yourNetID/file.txt would require execute permission on /, /u, and /home/yourNetID (as well as read permission on file.txt itself).&#x20;
* If you have execute permission on a directory, but not read permission, you can access a file in the directory if you know its name, but you can’t list the names of all entries in the directory.&#x20;
* To add or remove files in a directory, you need both execute and write permissions on the directory. Write permission without execute permission is completely meaningless.&#x20;
{% endhint %}

Here is a chart summarizing the properties of directory access permissions:\


| <p><br></p> | **List names of directory’s entries?**  | **Create, delete, rename directory’s files and empty directories or modify their metadata?**  | **Access directory entries? Make the directory your working directory? Display directory entries’ metadata?** |
| ----------- | --------------------------------------- | --------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| **`rwx`**   | ✔️                                      | ✔️                                                                                            | ✔️                                                                                                            |
| **`rw-`**   | ✔️                                      | ❌                                                                                             | ❌                                                                                                             |
| **`r-x`**   | ✔️                                      | ❌                                                                                             | ✔️                                                                                                            |
| **`-wx`**   | ❌                                       | ✔️                                                                                            | ✔️                                                                                                            |
| **`r--`**   | ✔️                                      | ❌                                                                                             | ❌                                                                                                             |
| **`-w-`**   | ❌                                       | ❌                                                                                             | ❌                                                                                                             |
| **`--x`**   | ❌                                       | ❌                                                                                             | ✔️                                                                                                            |
| **`---`**   | ❌                                       | ❌                                                                                             | ❌                                                                                                             |

## Displaying permissions on the command line

The three access permissions are denoted on the command line with three bits: `rwx`. `r` controls read access, `w` controls write access, and `x` controls execution. To display the permissions for all entries in the working directory, invoke ls `-l` on the command line:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 8.51.05 PM.png" alt=""><figcaption></figcaption></figure>

Here is another version with the relevant parts highlighted:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 8.50.55 PM.png" alt=""><figcaption></figcaption></figure>

As you can see, 10 bits are actually displayed, not 9. That’s because the first bit denotes the file type. For our purposes, we consider two types: ordinary files and directories. (Recall that a directory is a special type of file.) A `d` denotes a directory, while a `-` denotes an ordinary file. The next three sets of 3 bits denote the permissions for the owner, group, and all other users respectively.&#x20;

Let’s start with access permissions for `.git`, which are displayed as `drwxerxwrx`. The first bit, d, indicates that the entry is a directory. The `rwx` bits, which are enabled for all three groups—`sgewirtz`, `utemper`, and others—indicate that all users have read, write, and execute permissions.&#x20;

For the hello executable, the first bit, `-`, indicates that the file is an ordinary file. The subsequent 9 bits indicate that all users may read and execute `hello`, but only `sgewirtz` may modify it.&#x20;

Finally, for `hello.c`, none of the bits are enabled besides for the `r` and `w` bits for `sgewirtz`. Thus, no one may execute `hello`, and only `sgewirtz` may view or modify it. The lack of execution permission makes sense since `hello` is not an executable file.\
