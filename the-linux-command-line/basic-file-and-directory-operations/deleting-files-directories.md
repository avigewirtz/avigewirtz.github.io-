# Deleting Files/Directories

## Deleting files

To delete a file, use the `rm` (**r**e**m**ove) command followed by the name of the file you want to delete. For example, to delete `file1`, invoke:

```bash
rm file1
```

To delete multiple files, supply the name of each file as an argument to `rm`. For example:

```
rm file1 file2 file3
```

{% hint style="danger" %}
Deleting files and directories is a dangerous operation that should be exercised with caution. If you’re not careful, Linux will do exactly what you tell it to do, up to deleting every last one of your account's files and directories. The contents may not be recoverable.&#x20;

A sound approach is to invoke `rm` with the `-i` option, which prompts you for confirmation before deleting a file. Respond "y" to proceed and "n" to abort  For example:&#x20;

```bash
$ rm file1
remove file1? y
$
```

It's common practice to setup up your environment so that you are always prompted before deleting a file, even when you don't explicitly use the `-i` option. This is done by aliasing `rm` to `rm -i`. This alias is already set up on Armlab. To set it up on your PC, add the following line to the `.bashrc` file in your home directory:

```
alias rm='rm -i'
```

Going forward, if you attempt to delete a file, it'll prompt you for confirmation. If you are sure about deleting a file and do not want to be prompted, use the `-f` option:

```bash
$ rm -f file1
```
{% endhint %}

## Deleting directories

If the directory you want to delete is empty, you can use the `rmdir` (**r**e**m**ove **dir**ectory/ies) command. For example, to delete `dir1`:

```bash
rmdir dir1
```

To delete multiple directories, supply the name of each directory as an argument to `rmdir`. For example:&#x20;

```bash
rmdir dir1 dir2 dir2
```

`rmdir` only works for empty directories. If you attempt to delete a non-empty directory, you'll get the following error:&#x20;

```bash
$ rmdir dir1
rmdir: hgh: Directory not empty
$
```

### Deleting non-empty directories

To delete non-empty directories, you need to use the `rm` command with the `-r` option. For example, to delete `non_empty_dir`:

```bash
rm -r non_empty_dir
```

{% hint style="info" %}
It may seem that `rmdir` is redundant, since `rm -r` can handle both empty and non-empty directories. However, `rmdir` is safer because it ensures you do not accidentally delete non-empty directories.
{% endhint %}
