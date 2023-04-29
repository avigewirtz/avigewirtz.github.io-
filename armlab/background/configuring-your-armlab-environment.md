# Configuring your armlab environment

The first time you log into armlab, you will need to configure your environment. To do so, copy the following block and paste it into armlab:  &#x20;

{% code overflow="wrap" %}
```bash
[ "$SHELL" != "/bin/bash" ] && { echo "error: bash is not your login shell"; exit 1; }; \cp /u/cos217/.bash_profile /u/cos217/.bashrc /u/cos217/.emacs /u/cos217/.splintrc ~/; read -p "Enter your name: " name; read -p "Enter your email address: " email; git config --global user.name "$name"; git config --global user.email "$email"; git config --global core.editor emacs; git config --global color.ui auto; exec bash
```
{% endcode %}

If you get the message: `error: bash is not your login shell`, you must revisit [Activating Your armlab Account](activating-your-armlab-account.md) and complete step 2. If your shell is configured correctly, you will be prompted to enter your name and email address. This information will be used for Git configurations.&#x20;

Here's a breakdown of each command in the given code block:

```bash
[ "$SHELL" != "/bin/bash" ]: This checks if the current shell is not equal to /bin/bash (i.e., if the current shell is not Bash).
&&: This is a logical AND operator, which means the following block of commands will only execute if the previous condition ($SHELL != "/bin/bash") is true.
{ echo "error: bash is not your login shell"; exit 1; }: If the condition in step 1 is true, this block outputs an error message and exits the script with a non-zero status code (1) to indicate an error.
\cp /u/cos217/.bash_profile /u/cos217/.bashrc /u/cos217/.emacs /u/cos217/.splintrc ~/: This command copies the configuration files .bash_profile, .bashrc, .emacs, and .splintrc from the /u/cos217/ directory to the user's home directory (~/).
read -p "Enter your name: " name: This prompts the user to enter their name and stores it in the variable name.
read -p "Enter your email address: " email: This prompts the user to enter their email address and stores it in the variable email.
git config --global user.name "$name": This sets the user's name for Git configuration using the previously entered value.
git config --global user.email "$email": This sets the user's email address for Git configuration using the previously entered value.
git config --global core.editor emacs: This sets Emacs as the default text editor for Git.
git config --global color.ui auto: This enables automatic colorization of Git output in the terminal.
exec bash: This command replaces the current shell with a new instance of Bash, effectively reloading the shell and applying the updated configurations.
