# File and Directory Access Permissions

Earlier we covered the ls -l option, which lists the long format of each file in the working directory. The first column seems mysterious.&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-04-25 at 10.11.18 PM.png" alt=""><figcaption></figcaption></figure>

The column consists of 10 characters. The very first character distinguishes between a directory and a regular file: 'd' indicates a directory, and '-' signifies a regular file. The subsequent nine characters represent the file permissions, divided into three groups of three characters each. These groups correspond to the permissions for the file owner, the group, and others, respectively. Each group consists of three positions: the first for read permission ('r'), the second for write permission ('w'), and the third for execute permission ('x'). A dash ('-') in any of these positions means the corresponding permission is not granted.

* **Owner**: Typically the user who created the file, but ownership can be changed by the superuser.
* **Group**: A predefined group of users.&#x20;
* **Other**:  All other users.

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 8.50.55 PM.png" alt=""><figcaption></figcaption></figure>

For files, the meanings are pretty self-explanatory:&#x20;

* **Read**: The contents of the file may be read.&#x20;
* **Write**: The contents of the file may be modified.
* **Execute**: The (executable) file may be executed.&#x20;

For directories, the meanings are very confusing. The gist is as follows:

* **Read**: The names of the directory’s entries (i.e., files and subdirectories) may be listed (e.g., by using the ls command). Note that read permission on a directory only lets you view the file and directory names, but not their attributes (i.e., metadata). For that, you must have execute permissions.
* **Write**: Directory entries may be modified (i.e, created, deleted, and renamed and have their attributes modified.). Note that this only applies if the execute permission is also enabled. If execute is not enabled, write permission is totally meaningless.&#x20;
* **Execute**: Directory entries may be accessed, and you may make the directory your working directory. Note that if a directory cannot be accessed, neither can its children, regardless of your permissions for the children themselves. &#x20;

{% hint style="success" %}
To understand directory access permissions, it is helpful to recognize that a directory does not contain the contents of its file. It merely contains pointers to them. For example, if a directory contains the \<give example showing how it directory points to files and directoriues but doesn't contain their contents.>
{% endhint %}

Tips:

* If you have write and execute permissions on a directory, you can delete its files and empty directories even if you do not have any permission on the files or directories themselves.&#x20;
* To access a file or directory, execute permission is required on all of the directories in the pathname. For example, reading the file /u/yourNetID/file.txt would require execute permission on /, /u, and /home/yourNetID (as well as read permission on file.txt itself).&#x20;
* If you have execute permission on a directory, but not read permission, you can access a file in the directory if you know its name, but you can’t list the names of all entries in the directory.&#x20;
* To add or remove files in a directory, you need both execute and write permissions on the directory. Write permission without execute permission is completely meaningless.&#x20;

Here is a chart summarizing the properties of directory access permissions:\


<table data-header-hidden><thead><tr><th width="88"></th><th></th><th></th><th></th></tr></thead><tbody><tr><td><br></td><td><strong>Permisssion to list names of directory’s entries?</strong> </td><td><strong>Permission to create, delete, rename directory’s files and empty directories or modify their metadata?</strong> </td><td><strong>Permission to access directory entries? Make the directory your working directory? Display directory entries’ metadata?</strong></td></tr><tr><td><strong><code>rwx</code></strong></td><td>✔️</td><td>✔️</td><td>✔️</td></tr><tr><td><strong><code>rw-</code></strong></td><td>✔️</td><td>❌</td><td>❌</td></tr><tr><td><strong><code>r-x</code></strong></td><td>✔️</td><td>❌</td><td>✔️</td></tr><tr><td><strong><code>-wx</code></strong></td><td>❌</td><td>✔️</td><td>✔️</td></tr><tr><td><strong><code>r--</code></strong></td><td>✔️</td><td>❌</td><td>❌</td></tr><tr><td><strong><code>-w-</code></strong></td><td>❌</td><td>❌</td><td>❌</td></tr><tr><td><strong><code>--x</code></strong></td><td>❌</td><td>❌</td><td>✔️</td></tr><tr><td><strong><code>---</code></strong></td><td>❌</td><td>❌</td><td>❌</td></tr></tbody></table>
