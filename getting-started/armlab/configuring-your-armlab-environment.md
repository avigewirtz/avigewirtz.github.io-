# Configuring your armlab Environment

The first time you log into armlab, you will need to configure your environment. To do so, copy the following code block and paste it into armlab. At this early stage of the semester you are not expected to understand the specifics of how this code block works. However, if you're interested in having a high-level understanding, a commented version of the code block is provided below. &#x20;

{% code overflow="wrap" %}
```bash
{ if [ "$SHELL" != "/bin/bash" ]; then echo "Error: bash is not your login shell"; else \cp /u/cos217/.bash_profile ~/; \cp /u/cos217/.bashrc ~/; \cp /u/cos217/.emacs ~/; \cp /u/cos217/.splintrc ~/; read -p "Enter your name: " name; read -p "Enter your email address: " email; git config --global user.name "$name"; git config --global user.email "$email"; git config --global core.editor emacs; git config --global color.ui auto; exec bash; fi; }
```
{% endcode %}

If you get the message: `error: bash is not your login shell`, you must revisit [Activating Your armlab Account](activating-your-armlab-account.md) and complete step 2. Otherwise, you will be prompted to enter your name and email address. This information will be used to configure Git.

<details>

<summary>Commented Version</summary>

```bash
{
    # If the login shell is not bash, prints an error message
    if [ "$SHELL" != "/bin/bash" ]; then
        echo "Error: bash is not your login shell"
    else
        # Copies the .bash_profile file from the /u/cos217/ directory 
        # to the user's home directory (~)
        \cp /u/cos217/.bash_profile ~/

        # Copies the .bashrc file from the /u/cos217/ directory to the 
        # user's home directory (~)
        \cp /u/cos217/.bashrc ~/

        # Copies the .emacs file from the /u/cos217/ directory to the 
        # user's home directory (~)
        \cp /u/cos217/.emacs ~/

        # Copies the .splintrc file from the /u/cos217/ directory to the 
        # user's home directory (~)
        \cp /u/cos217/.splintrc ~/

        # Prompts the user to enter their name and store it in the 
        # "name" variable
        read -p "Enter your name: " name

        # Prompts the user to enter their email address and store it in 
        # the "email" variable
        read -p "Enter your email address: " email
        
        # Configures Git with the user's name
        git config --global user.name "$name"

        # Configures Git with the user's email address
        git config --global user.email "$email"

        # Configures Git to use Emacs as the default text editor
        git config --global core.editor emacs

        # Configures Git to enable colored output
        git config --global color.ui auto

        # Starts a new instance of the Bash shell
        exec bash
    fi
}
```

</details>

