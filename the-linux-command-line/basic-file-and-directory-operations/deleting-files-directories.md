# Deleting Files/Directories

## Deleting files

\<fill in>

{% hint style="danger" %}
Deleting files and directories is a dangerous operation that should be exercised with caution. If you’re not careful, Linux will do exactly what you tell it to do, up to deleting every last one of your account's files and directories. The contents may not be recoverable.&#x20;

A good approach is to invoke `rm` with the `-i` option, which prompts you for confirmation before deleting a file. Respond "y" to proceed and "n" to abort  For example:&#x20;

```bash
$ rm file1
remove file1? y
$
```

A common practice is to setup up your environment so that a confirmation prompt is the default. This is done by aliasing `rm` to `rm -i`. This alias is already set up for your account on Armlab. To set it up on your PC, add the following line to the `.bashrc` file in your home directory:

```
alias rm='rm -i'
```

Going forward, if you attempt to delete a file, it'll prompt you for confirmation. If you are sure about deleting a file and do not want to be prompted, use the `-f` option:

```bash
$ rm -f file1
```
{% endhint %}

## Deleting directories

If the directory you want to delete is empty, you can use the `rmdir` (**r**e**m**ove **dir**ectory/ies) command. For example:

```bash
rmdir dir1
```

You can also delete multiple directories via a single invocation of rmdir. For example:

```bash
rmdir dir1 dir2 dir2
```

If the directory you want to delete is not empty, `rmdir` will not work. You will get the following error:

### Deleting non-empty directories

To delete non-empty directories, use the `rm` command with the `-r` option. For example:

```bash
rm -r dir1 
```

{% hint style="info" %}
It may seem that rmdir is redundant, since \<fill in>
{% endhint %}
