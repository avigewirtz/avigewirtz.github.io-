# Deleting Files and Directories

Deleting files and directories can be accomplished with the `rm` command. Its syntax is as follows: <mark style="color:red;">**`rm`**</mark><mark style="color:green;">**`OPTION(S)`**</mark><mark style="color:blue;">**`FILES/DIRECTORY(IES)`**</mark>.&#x20;

The <mark style="color:blue;">**FILES/DIRECTORY(IES)**</mark> parameter represents the files or directories you want to delete. By default, the `rm` command only deletes files. To use it to delete directories, you must supply the `-r` option (i.e., `rm -r DIRECTORY(IES)`.&#x20;

While both empty and nonempty files and directories can be deleted with the `rm` command, you can also use the `rmdir` command to delete empty directories. The benefit of using the `rmdir` command to delete directories is it provides a more explicit and cautious approach to deleting directories. By restricting itself to empty directories, it helps prevent accidental deletion of nonempty directories and their contents.

### Common options

* **`-r`**: Deletes directory(ies), even if they are not empty.
* **`-i`**: Prompts the user for confirmation before deleting each file/directory.&#x20;
* **`-f`**: Overrides `-i` option (i.e., removes confirmation prompt).

{% hint style="danger" %}
Deleting files and directories is a dangerous operation. If you’re not careful, the operating system will do exactly what you tell it to, including destroying every last one of your files and directories. For this reason, deleting non-empty files or non-empty directories is deliberately made difficult.&#x20;
{% endhint %}

### Exercises

1. Delete _dir1_ using `rmdir`:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 4.22.41 PM.png" alt=""><figcaption></figcaption></figure>

The operation succeeds since _dir1_ is empty.

2. Delete _dir2_ using `rmdir`:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 4.23.00 PM.png" alt=""><figcaption></figcaption></figure>

The operation fails since _dir2_ is not empty.&#x20;

3. Let's clean things up a bit. Delete _dir3_, _dir4_, _bad_, _name_, and '_bad name_':

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 4.23.11 PM.png" alt=""><figcaption></figcaption></figure>

4. Delete _file1_:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 4.29.21 PM.png" alt=""><figcaption></figcaption></figure>

The prompt `rm: remove regular empty file 'file1'?`  is displayed because on Armlab, `rm` is aliased to `rm -i`.&#x20;

2. Delete _dir2_:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 4.29.29 PM.png" alt=""><figcaption></figcaption></figure>

3. Delete _file3_ and _file4_ using the `-f` option, which removes the confirmation prompt:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 4.29.39 PM.png" alt=""><figcaption></figcaption></figure>



