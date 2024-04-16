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

When you commit changes to a Git repository, Git associates with your commit records your username and email. By default, Git uses the username and email address associated with your user account on your local machine. However, you can change the default email and username using the above configurations.&#x20;

* git config --global core.editor “yourPreferredEditor''

When you run git commit without a -m option, Git opens up a text editor for you to enter a commit message describing the changes you have made. By default, Git uses the system's default text editor, which may not be your editor of choice. You can change the default editor using the above configuration.&#x20;

* git config --global color.ui auto&#x20;

When you run certain Git commands in the terminal, Git can use color output to make the output easier to read and understand. For example, the output of git diff can be colorized to show changes more clearly. The above configuration sets color output for Git commands on your local machine.

