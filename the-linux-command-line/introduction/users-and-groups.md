# Users Accounts

User accounts enable Linux to tailor the computing environment based on who is logged in. This is for securtiy, such as ensuring one user doesn't access another user's files, and convinience.&#x20;

A typical user account consists of the following information:

* [Username and user ID (UID)](https://www.microfocus.com/documentation/open-enterprise-server/2023/acc\_linux\_svcs\_lx/bx3sbhf.html#bx3tloq)
* [Password](https://www.microfocus.com/documentation/open-enterprise-server/2023/acc\_linux\_svcs\_lx/bx3sbhf.html#bx3tlyx)
* [Primary group name and group ID (GID)](https://www.microfocus.com/documentation/open-enterprise-server/2023/acc\_linux\_svcs\_lx/bx3sbhf.html#bx3tmat)
* [Secondary group names and group IDs](https://www.microfocus.com/documentation/open-enterprise-server/2023/acc\_linux\_svcs\_lx/bx3sbhf.html#bx3tmql)
* [Location of the home directory](https://www.microfocus.com/documentation/open-enterprise-server/2023/acc\_linux\_svcs\_lx/bx3sbhf.html#bx3tn3f)
* [Preferred shell](https://www.microfocus.com/documentation/open-enterprise-server/2023/acc\_linux\_svcs\_lx/bx3sbhf.html#bx3tnbh)

## Viewing account information

You can find out the information of your user account via the id command. When I invoke it on armlab, I get the following output:

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-27 at 11.56.24 PM.png" alt=""><figcaption></figcaption></figure>

Here's what each part of the highlighted part means:

* `uid=127000(sgewirtz)`: MY UID is _127000_ and my username is _sgewirtz_.&#x20;
* `gid=35(utempter)`: My primary group is utemper, with GID 35.&#x20;
* `groups=35(utempter)`: This part of the output lists all the groups that I belong to, which is only one group (_utemper_).&#x20;

You can safely ignore the rest of the output, which has to do with sellinux.&#x20;

It goes without saying that Linux must have some scheme to uniquely identify each user.&#x20;

### Users

Each user is identified by a unique login name and a corresponding numeric _User ID_ (UID). UIDs are usually assigned by the system administrator, with normal users having UIDs above 500. The system administrator, also known as the superuser or root user, has a UID of 0 and typically uses the username _root_.

User information, including the username, UID, and other details, are stored in the _/etc/passwd_ file. Each line in this file represents a user and contains the following fields separated by colons:

```bash
username:password:UID:GID:comment:home_directory:shell
```

### Groups

In certain situations, it is convenient to treat a set of users as a single entity. For example, a teacher might want to treat all students in a class as a single entity for the purpose of granting access to a common set of files.&#x20;

This can be done by associating a list of usernames with a single group. Each group has a unique group name and a corresponding numeric _Group ID_ (GID). A user can belong to multiple groups, and group membership is defined by the system administrator.

Group information is stored in the _/etc/group_ file. Each line in this file represents a group and contains the following fields separated by colons:

```makefile
group_name:password:GID:user_list
```

## Viewing user and group information

You can display your login name, group name, UID, and GID by issuing the `id` command. When I issue it on armlab, I get the following output:

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-27 at 11.56.24 PM.png" alt=""><figcaption></figcaption></figure>

Let's break this down:

* `uid=127000(sgewirtz)`: This part of the output shows my User ID (_127000_) and my username (_sgewirtz_).&#x20;
* `gid=35(utempter)`: This part of the output shows my primary Group ID (_35_) and the associated group name (_utemper_).&#x20;
* `groups=35(utempter)`: This part of the output lists all the groups that I belong to, which is only one group (_utemper_).&#x20;
* `context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023`: This part of the output displays the SELinux (Security-Enhanced Linux) context associated with the user. SELinux is a security feature in Linux that enforces access control policies, the details of which are not important for our discussion.&#x20;
