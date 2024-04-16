# Installing Git

In COS217, there is no need to install Git, since Git is already installed on Armlab. However, if you'd like to have Git on your PC as well, you can install it by following the instructions below.&#x20;

{% tabs %}
{% tab title="macOS" %}
There are many ways to install Git on macOS. The easiest method is by installing the _Xcode Command Line Tools_, which includes a version of Git.

Run the following command in Terminal:&#x20;

```bash
git --verion
```

If Git is already installed, the command will output `git version X.Y.Z`. Otherwise, it will prompt you to install Xcode Command Line Tools.&#x20;

{% hint style="info" %}
Note that the version of Git included with Xcode is not necessarily the latest version. If you specifically want the latest version, download Git using the official Git [installer](https://git-scm.com/download/mac).&#x20;
{% endhint %}
{% endtab %}

{% tab title="Windows" %}
In the Command Prompt, enter the following command:

```bash
git --version
```

If a Git version number is returned, it means Git is installed. If an error is returned, it means Git is not installed. Navigate to http://git-scm.com/download/win, and the installation will start automatically.
{% endtab %}
{% endtabs %}
