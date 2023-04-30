# Users and Groups

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
