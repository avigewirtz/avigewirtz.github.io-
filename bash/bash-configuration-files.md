# Bash Configuration Files

When a user logs in or out of a Bash terminal session, various Bash configuration files are automatically executed.&#x20;

## Login configuration files

These files define the user's environment, initializing variables, aliases, and functions. The main login configuration files include`/etc/profile`, `~/.bash_profile` or `~/.profile`.&#x20;

* `/etc/profile`: This is a global configuration file that is executed when a user logs into the system using a Bash shell. It sets up system-wide environment variables, such as the `PATH`, and is generally used for defining global settings that apply to all users.
* `~/.bash_profile` or `~/.profile`: These are user-specific configuration files that are executed when a user logs in with a Bash login shell. They are used to set up user-specific environment variables, aliases, and functions. If both files exist, `~/.bash_profile` takes precedence.

Upon login, these files are executed in the following order:

1. `/etc/profile`
2. `~/.bash_profile` or `~/.profile`

If there is a conflict between any two configuration files, the one executed second will override the previously executed one. So, for example, if there is a conflict between `/etc/profile` and  `~/.bash_profile` or `~/.profile`, the latter will override the former.

## Logout configuration file

When a user logs out of a bash terminal session, the `~/.bash_logout` configuration file is executed. This performs cleanup tasks, such as clearing the terminal and saving command history.

{% hint style="info" %}
You can view the contents of configuration files by using any of the [file viewing commands](viewing-files.md), such as `cat` or `emacs`. Understanding these configuration files enables you to customize the behavior and appearance of your Bash terminal sessions.
{% endhint %}
