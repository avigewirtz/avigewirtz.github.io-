---
description: >-
  This page explains Linux file and directory access permissions: read, write,
  execute.
---

# File and Directory Access Permissions

Associated with each file and directory are three categories of users to whom access permissions may be granted: &#x20;

* **Owner**: Typically the user who created the file, but ownership can be changed by the superuser.
* **Group**: A predefined group of users.&#x20;
* **Other**:  All other users.

Each of these user categories may be granted three types of permissions: read, write, and execute. In this section, we will go over how to view and interpret these access permissions. &#x20;

### Viewing access permissions

You can view the permissions of each of user category via the `ls -l` command, which lists the directory's entries in long format. Here's an example of the sort of output you might get:

```
$ ls -l
drwxr-xr-x  3  sgewirtz  utempter    68  Jun 26  15:37  public_html
-rw-r--r--  1  sgewirtz  utempter  4017  Feb 17  2023   index.html
```

The parts relevant to our discussion are summarized in Figure 13.

<figure><img src="../.gitbook/assets/Frame 1 (3).png" alt=""><figcaption></figcaption></figure>

Of most interest is the first column. The first character indicates the file type--`d` for a directory, and `-` for an ordinary file. There are other types of files, but that's beyond our scope.&#x20;

The subsequent nine characters, divided into three groups of three, indicate read (`r`), write (`w`), and execute (`x`) permissions for _owner_, _group_, and _other_ respectively. The presence of an `r`, `w`, or `x` n any of these positions indicates that's the corresponding permission is granted. A `-` indicates that the corresponding permission is not granted.&#x20;

### **Interpreting File Access Permissions**

The precise meanings of read, write, and execute permissions differs for files and directories. For files, the meanings are pretty self-explanatory:&#x20;

* **Read**: The contents of the file may be read. For example, you can use the `cat` command to print the file's contents on stdout.&#x20;
* **Write**: The contents of the file may be modified. For example, you can use an editor like Emacs to edit the file's contents.&#x20;
* **Execute**: The file may be executed. (explain)

### **Interpreting Directory Access Permissions**

For directories, the meanings are extremely confusing. The gist is as follows:

* **Read**: The directory’s entries may be listed (e.g., by invoking the `ls` command). Note that this permission only allows you to view the names of the directory's entries. It does not allow you to view the entries' metadata (e.g., via `ls -l)`. To view the metadata, you must have execute permissions.&#x20;
* **Write**: Directory entries may be modified (i.e, created, deleted, renamed, and have their attributes modified.). Note that this only applies if the execute permission is also enabled. If execute is not enabled, write permission is totally meaningless.&#x20;
* **Execute**: Directory entries may be accessed, and you may make the directory your working directory. Note that if a directory cannot be accessed, neither can its children, regardless of your permissions for the children themselves. &#x20;

#### Gotchas

Permissions are extremely confusing and not intuitive, so we'll go over some directory access permission gotchas.&#x20;

* You may view the metadata of a file in a directory even if you don't have read (or write) permission on the directory. However, you must know the exact path or name of the child directory, as you won’t be able to obtain this information from listing the contents of the parent directory.
* If you have read permission on a child directory, you can list it's contents, even if you don't have read permission on its parent. Here too you must know the exact path or name of the child directory.
* If you have write and execute permissions on a directory, you can delete its files and empty directories even if you do not have any permissions for the files or directories themselves.&#x20;
* To access a file or directory, execute permission is required on all of the directories in the pathname. For example, reading the file /u/yourNetID/file.txt would require execute permission on /, /u, and /home/yourNetID (as well as read permission on file.txt itself).&#x20;
* To add or remove files in a directory, you need both execute and write permissions on the directory. Write permission without execute permission is completely meaningless.&#x20;

Here is a chart summarizing the properties of directory access permissions:\


<table data-header-hidden><thead><tr><th width="88"></th><th></th><th></th><th></th></tr></thead><tbody><tr><td><br>Directory name = directory</td><td>Permission to list directory entries?</td><td><strong>Permission to create, delete, rename directory’s files and empty directories or modify their metadata?</strong> </td><td><strong>Permission to access directory entries? Make the directory your working directory? Display directory entries’ metadata?</strong></td></tr><tr><td><strong><code>rwx</code></strong></td><td>✔️</td><td>✔️</td><td>✔️</td></tr><tr><td><strong><code>rw-</code></strong></td><td>✔️</td><td>❌</td><td>❌</td></tr><tr><td><strong><code>r-x</code></strong></td><td>✔️</td><td>❌</td><td>✔️ </td></tr><tr><td><strong><code>-wx</code></strong></td><td>❌</td><td>✔️</td><td>✔️</td></tr><tr><td><strong><code>r--</code></strong></td><td>✔️</td><td>❌</td><td>❌</td></tr><tr><td><strong><code>-w-</code></strong></td><td>❌</td><td>❌</td><td>❌</td></tr><tr><td><strong><code>--x</code></strong></td><td>❌</td><td>❌</td><td>✔️</td></tr><tr><td><strong><code>---</code></strong></td><td>❌</td><td>❌</td><td>❌</td></tr></tbody></table>

## Exercises

1. What does the permission code `drwxr-x---` on a directory allow the owner of the directory to do?
   * A) Execute files only
   * B) Read, write, and execute files
   * C) Read and execute files, but not write
   * D) Read, write, and execute within the directory
   * E) None of the above
2. Which of the following permissions allow a user group to enter a directory and read files if the filenames are known, but not list the contents of the directory?
   * A) `drw-------`
   * B) `dr-x------`
   * C) `d---r-x---`
   * D) `d----x----`
   * E) `drwxr-xr-x`
3. If a file within a directory has the permissions `-rw-rw-r--`, which actions are true for a user who is not the owner but is part of the group?
   * A) Can execute the file
   * B) Can read the file
   * C) Can modify the file
   * D) Can delete the file
   * E) B and C
4. A directory has the permission code `drwxrwx--x`. What can a user, who is not the owner or a part of the group associated with the directory, do?
   * A) Create new files within the directory
   * B) Delete files within the directory
   * C) Enter the directory
   * D) List all files within the directory
   * E) None of the above
5. Which permission setting on a file ensures that only the file owner can read and write, but everyone else can only execute?
   * A) `-rwx--x--x`
   * B) `-rw-r-xr-x`
   * C) `-rw-------`
   * D) `-rwxr-x---`
   * E) `-rw-r--r-x`
6. What happens if you try to execute a script that you have read permission for, but not execute permission, in a directory where you have execute permission?
   * A) The script runs without any issues
   * B) The script does not run, and you get a permission denied error
   * C) The script's contents are displayed in the terminal
   * D) The script is automatically given execute permission
   * E) None of the above
7. For a directory with the permissions `drwxr-s---`, which statement is true?
   * A) The setuid bit is set, allowing files to be executed as the owner
   * B) The setgid bit is set, making new files inherit the directory's group
   * C) Users not in the group cannot access the directory at all
   * D) B and C
   * E) All of the above
8. When a directory has the permission `drwx--x--x`, which tasks can a user, who is neither the owner nor a group member, perform?
   * A) Read files in the directory if the names are known
   * B) List the contents of the directory
   * C) Change into the directory
   * D) Modify files in the directory if the names are known
   * E) A and C

<details>

<summary>Answers to exercises </summary>

1. &#x20; D) Read, write, and execute within the directory
2. &#x20; D) `d----x----`
3. &#x20; E) B and C
4. &#x20; C) Ensures only the owner can delete or rename files within the directory
5. &#x20; B) `chown`
6. &#x20; C) Enter the directory
7. &#x20; A) `-rwx--x--x`
8. &#x20; B) The script does not run, and you get a permission denied error
9. &#x20; D) B and C
10. C) Change into the directory

</details>
