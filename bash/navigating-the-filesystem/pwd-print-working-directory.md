# Printing Working Directory

The `pwd` command is a simple yet powerful command, used to determine the [absolute pathname](../../linux-filesystem/filesystem/pathnames.md#absolute-pathnames) of your [working directory](../../linux-filesystem/filesystem/notable-directories.md#working-directory).

Upon logging into Linux, your [home directory](../../linux-filesystem/filesystem/notable-directories.md#home-directory) will by default be set as your working directory. To verify this, [log into](../../armlab/logging-into-armlab/#logging-into-armlab) Armlab and invoke:

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.08.38 PM.png" alt=""><figcaption></figcaption></figure>

Your output should be _/u/yourNetID_, which is the absolute pathname of your home directory.

{% hint style="success" %}
On Armlab, the working directory is displayed in the [shell prompt](../warm-up-commands.md#shell-prompt), between the colon (:) and dollar ($) sign. In the above example, the prompt shows that the working directory is \~ (tilde), which represents the home directory.
{% endhint %}
