# Deleting Files and Directories

There are two commands for deleting files and directories: one for deleting empty directories only, and the other for deleting everything else.

{% hint style="danger" %}
Deleting non-empty files or non-empty directories is a dangerous operation. If you’re not careful, the operating system will do exactly what you tell it to do, including destroying every last one of your files and directories. For this reason, deleting non-empty files and directories is deliberately made difficult.&#x20;
{% endhint %}



## Deleting empty directories

### Examples

1. Delete `dir1`:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 4.22.41 PM.png" alt=""><figcaption></figcaption></figure>

The operation succeeds since `dir1` is empty.

2. Delete `dir2`:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 4.23.00 PM.png" alt=""><figcaption></figcaption></figure>

The operation fails since `dir2` is not empty.&#x20;

3. Let's clean things up a bit. Delete `dir3`, `dir4`, `bad`, `name`, and `bad name`:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 4.23.11 PM.png" alt=""><figcaption></figcaption></figure>

## Deleting files and non-empty directories



### Syntax: <mark style="color:red;">`rm`</mark>` `<mark style="color:green;">`OPTION(S)`</mark>` `<mark style="color:blue;">`FILES/DIRECTORY(IES)`</mark>&#x20;

### Common options

* &#x20;\-r   —   deletes directory(ies), even if they are not empty.
* &#x20;\-i   —   prompts the user for confirmation before deleting each file.&#x20;
* &#x20;\-f   —   overrides -i option (i.e., removes confirmation prompt).

### Examples

1. Delete `file1`:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 4.29.21 PM.png" alt=""><figcaption></figcaption></figure>

The prompt “rm: remove regular empty file 'file1'?”  is displayed because rm is aliased to “rm -i”.&#x20;

2. Delete `dir2`:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 4.29.29 PM.png" alt=""><figcaption></figcaption></figure>

3. Delete `file3` and `file4`, but remove the confirmation prompt:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 4.29.39 PM.png" alt=""><figcaption></figcaption></figure>

