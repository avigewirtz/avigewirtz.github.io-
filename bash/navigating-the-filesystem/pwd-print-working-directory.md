# pwd (Print Working Directory)

The `pwd` command is a simple yet powerful command used to determine the absolute pathname of the working directory.

Upon logging into armlab, your home directory will by default be your working directory. To verify this, [log into](../../armlab/background/logging-into-armlab/#logging-into-armlab) armlab and invoke:

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-25 at 10.08.38 PM.png" alt=""><figcaption></figcaption></figure>

Your output should be _/u/yourNetID_, which is the absolute pathname of your home directory.&#x20;

{% hint style="success" %}
A useful feature of the shell is that the working directory can be displayed in the shell prompt. On armlab, the working directory is displayed in the shell prompt between the colon and dollar sign. In the above example, the working directory is \~ (tilde). (Recall that \~ represents your home directory.) Using that knowledge, you determine the working directory by simply inspecting the shell prompt.&#x20;
{% endhint %}
