# Users and Groups

Each user on the system is uniquely identified, and users may belong to groups.

#### Users

Every user of the system has a unique login name (username) and a corresponding numeric user ID (UID). For each user, these are defined by a line in the system password file, /etc/passwd, which includes the following additional information:

* Group ID: the numeric group ID of the first of the groups of which the user is a member.
* Home directory: the initial directory into which the user is placed after logging in.
* Login shell: the name of the program to be executed to interpret user commands.

The password record may also include the user’s password, in encrypted form. However, for security reasons, the password is often stored in the separate shadow password file, which is readable only by privileged users.

#### Groups

In certain situations, such as for controlling access to certain files and system resources, it is convenient to treat a set of users as a single entity. For example, a teacher might want to treat all students in a class as a single entity for the purpose of granting access to a common set of files.&#x20;

This can be done by associating a list of usernames with a single group. Each group has a unique group name and a corresponding numeric _Group ID_ (GID). A user can belong to multiple groups, and group membership is defined by the system administrator.

Group information is stored in the _/etc/group_ file. Each line in this file represents a group and contains the following fields separated by colons:

```makefile
group_name:password:GID:user_list
```

Each user automatically has a primary group. Optionally, they may have secondary groups.&#x20;











For administrative purposes—in particular, for controlling access to files and other system resources—it is useful to organize users into groups. For example, the people in a team working on a single project, and thus sharing a common set of files, might all be made members of the same group. Each group is identified by a single line in the system group file, /etc/group, which includes the following information:

* Group name: the (unique) name of the group.
* Group ID (GID): the numeric ID associated with this group.
* User list: a comma-separated list of login names of users who are members of this group (and who are not otherwise identified as members of the group by virtue of the group ID field of their password file record).

{% hint style="info" %}
**Superuser**

One user, known as the superuser, has special privileges within the system. The superuser account has user ID 0, and normally has the login name root. On typical UNIX systems, the superuser bypasses all permission checks in the system. Thus, for example, the superuser can access any file in the system, regardless of the per- missions on that file, and can send signals to any user process in the system. The system administrator uses the superuser account to perform various administrative tasks on the system.
{% endhint %}



Each user has their own account. Allows Linux to tailor environment to you,&#x20;





To access a Linux system you must login. User accounts enable Linux to tailor the computing environment based on who is logged in. This is for security, such as ensuring one user doesn't access another user's files, and convenience.&#x20;

### Users

Each user is identified by a unique login name and a corresponding numeric _User ID_ (UID). UIDs are usually assigned by the system administrator, with normal users having UIDs above 500. The system administrator, also known as the superuser or root user, has a UID of 0 and typically uses the username _root_.

Some mention of login and Password here

User information, including the username, UID, and other details, are stored in the _/etc/passwd_ file. Each line in this file represents a user and contains the following fields separated by colons:

```bash
username:password:UID:GID:comment:home_directory:shell
```

additional info associated with each account:

* Location of the home directory
* Preferred shell

### Groups

In certain situations, it is convenient to treat a set of users as a single entity. For example, a teacher might want to treat all students in a class as a single entity for the purpose of granting access to a common set of files.&#x20;

This can be done by associating a list of usernames with a single group. Each group has a unique group name and a corresponding numeric _Group ID_ (GID). A user can belong to multiple groups, and group membership is defined by the system administrator.

Group information is stored in the _/etc/group_ file. Each line in this file represents a group and contains the following fields separated by colons:

```makefile
group_name:password:GID:user_list
```

Each user automatically has a primary group. Optionally, they may have secondary groups.&#x20;

## Viewing user and group information

You can display your login name, group name, UID, and GID by issuing the `id` command. When I invoke `id` on Armlab, I get the following output:

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-27 at 11.56.24 PM.png" alt=""><figcaption></figcaption></figure>

Let's break down the first row:&#x20;

* `uid=127000(sgewirtz)`: This part of the output shows my User ID (_127000_) and my username (_sgewirtz_).&#x20;
* `gid=35(utempter)`: This part of the output shows my primary Group ID (_35_) along with its name (_utemper_).&#x20;
* `groups=35(utempter)`: This part of the output lists all the groups that I belong to, which is only one group (_utemper_).&#x20;

You can safely ignore the output on the second row.&#x20;

