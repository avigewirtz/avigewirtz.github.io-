# Users Accounts

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

<figure><img src="../.gitbook/assets/Screenshot 2023-04-27 at 11.56.24 PM.png" alt=""><figcaption></figcaption></figure>

Let's break down the first row:&#x20;

* `uid=127000(sgewirtz)`: This part of the output shows my User ID (_127000_) and my username (_sgewirtz_).&#x20;
* `gid=35(utempter)`: This part of the output shows my primary Group ID (_35_) along with its name (_utemper_).&#x20;
* `groups=35(utempter)`: This part of the output lists all the groups that I belong to, which is only one group (_utemper_).&#x20;

You can safely ignore the output on the second row.&#x20;

