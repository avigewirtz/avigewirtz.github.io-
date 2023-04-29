# Users and Groups

Linux is a multiuser operating system. In simple terms, that means that a single Linux computer can be shared by many users, all of whom may be logged in at any time–even simultaneously. It goes without saying that we must have some way of uniquely identifying each user on the system.&#x20;

{% hint style="info" %}
If the idea of a multiuser computer seems foreign or reminiscent of the Stone Age when computers were as large and expensive as cars and had to be shared by entire organizations, recall that Armlab is shared by hundreds of students and faculty (some of whom might be logged in the same time that you are).
{% endhint %}

### Users

Each user has a unique login name and a corresponding numeric user ID (UID). UIDs are normally over 500 and are assigned by the system administrator. The system administrator, also known as the superuser, has user ID 0, and normally has the username root.&#x20;

### Groups

In certain situations, it is convenient to treat a set of users as a single entity. For example, we might want to treat all students in a course as a single entity for the purpose of granting access to a common set of files. We do this by associating a list of usernames with a single group. Each group has a unique group name and a corresponding numeric group ID (GID). A user can simultaneously belong to multiple groups. Groups are defined by the system administrator.&#x20;

You can display your login name, group name, UID, and GID by issuing the id command:

The relevant part is highlighted.

<figure><img src="../.gitbook/assets/Screenshot 2023-04-27 at 11.56.24 PM.png" alt=""><figcaption></figcaption></figure>

\
\
