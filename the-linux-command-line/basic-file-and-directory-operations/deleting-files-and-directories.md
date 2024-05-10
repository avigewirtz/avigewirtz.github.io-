# Deleting Files and Directories

### Deleting Files

To delete a file, type `rm` (**r**e**m**ove) followed by the name of the file you want to delete. For example, to delete `file1`:

```bash
rm file1
```

To delete multiple files, supply the name of each file you want to delete as an argument to `rm`. For example, to delete `file1`, `file2`, and `file3`:

```bash
rm file2 file3 file4
```

{% hint style="danger" %}
Deleting files and directories is a dangerous operation that should be exercised with caution. If you’re not careful, Linux will do exactly what you tell it to, up to deleting every last one of your files and directories. The contents may not be recoverable.

A wise approach is to always invoke `rm` with the `-i` option, which prompts you for confirmation before deleting a file. Respond "y" to proceed and "n" to abort For example:

```bash
$ rm -i file1
remove file1? y
$
```

It's common practice to alias `rm` to `rm -i`, ensuring you're always prompted for confirmation before deleting a file. This alias is already set up on Armlab. You can set it up on your PC by adding the following line to your `.bashrc` file:

```
alias rm='rm -i'
```

If you are sure about deleting a file and do not want to be prompted for confirmation, you can override `-i` with the`-f` (force) option:

```bash
$ rm -f file1
```
{% endhint %}

### Deleting Empty Directories

If the directory you want to delete is empty, you can use the `rmdir` (**r**e**m**ove **dir**ectory/ies) command. Type `rmdir` followed by the name of the directory you want to delete. For example, to delete `dir1`:

```bash
rmdir dir1
```

To delete multiple empty directories, supply the name of each directory as an argument to `rmdir`. For example, do delete `dir2`, `dir3`, and `dir4`:

```bash
rmdir dir2 dir3 dir4
```

{% hint style="warning" %}
If you attempt to delete a non-empty directory with `rmdir`, you'll get an error:

```bash
$ rmdir dir1
rmdir: dir1: Directory not empty
$
```
{% endhint %}

### Deleting Non-empty Directories

To delete non-empty directories, use the `rm` command with the `-r` option. For example, to delete `non_empty_dir`:

```bash
rm -r non_empty_dir
```

{% hint style="info" %}
It may seem that `rmdir` is redundant, since `rm -r` can handle both empty and non-empty directories. However, `rmdir` is safer because it ensures you do not accidentally delete non-empty directories.
{% endhint %}
