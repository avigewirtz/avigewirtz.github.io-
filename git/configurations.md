# Configurations

* git config --global user.name “yourName” / git config --global user.email “yourEmailAddress”:

When you commit changes to a Git repository, Git associates with your commit records your username and email. By default, Git uses the username and email address associated with your user account on your local machine. However, you can change the default email and username using the above configurations.&#x20;

* git config --global core.editor “yourPreferredEditor''

When you run git commit without a -m option, Git opens up a text editor for you to enter a commit message describing the changes you have made. By default, Git uses the system's default text editor, which may not be your editor of choice. You can change the default editor using the above configuration.&#x20;

* git config --global color.ui auto&#x20;

When you run certain Git commands in the terminal, Git can use color output to make the output easier to read and understand. For example, the output of git diff can be colorized to show changes more clearly. The above configuration sets color output for Git commands on your local machine.
