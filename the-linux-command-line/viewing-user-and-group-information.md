# Viewing User and Group Information

You can display your login name, group name, UID, and GID by issuing the `id` command. When I invoke `id` on Armlab, I get the following output:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-27 at 11.56.24 PM.png" alt=""><figcaption></figcaption></figure>

Let's break down the first row:&#x20;

* `uid=127000(sgewirtz)`: This part of the output shows my User ID (_127000_) and my username (_sgewirtz_).&#x20;
* `gid=35(utempter)`: This part of the output shows my primary Group ID (_35_) along with its name (_utemper_).&#x20;
* `groups=35(utempter)`: This part of the output lists all the groups that I belong to, which is only one group (_utemper_).&#x20;

You can safely ignore the output on the second row.&#x20;
