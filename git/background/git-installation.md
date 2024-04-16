# Setting Up Your Git/GitHub Environment

## Installing Git

In COS217, there is no need to install Git, since Git is already installed on Armlab. However, if you'd like to obtain Git on your PC as well, you can install it by following the instructions below.&#x20;

{% tabs %}
{% tab title="macOS" %}
There are many ways to install Git on macOS. The easiest method is by installing the _Xcode Command Line Tools_, which includes a version of Git

* Run the following command in Terminal: `git -v`. If Git is already installed, the command will output `git version X.Y.Z`. Otherwise, it will prompt you to install Xcode Command Line Tools.

{% hint style="info" %}
Note that the version of Git included with Xcode is not necessarily the latest version. If you specifically want the latest version, download Git using the official Git [installer](https://git-scm.com/download/mac).&#x20;
{% endhint %}
{% endtab %}

{% tab title="Windows" %}
You may already have Git installed thanks to the introcs infrastructure from COS 126, which installs Git Bash. If this is not the case, navigate to http://git- scm.com/download/win, and the installation will start automatically.
{% endtab %}
{% endtabs %}

## Setting Git configurations

```bash
git config --global user.name YOUR_NAME
git config --global user.email YOUR_EMAIL_ADDRESS 
git config --global core.editor NAME_OF_PREFFERED_EDITOR
```

For example:

```bash
git config --global user.name John Smith
git config --global user.email johnsmith@gmail.com
git config --global core.editor emacs
```

