# Configuring Your Armlab Environment

The first time you log into Armlab, you will need to configure your environment. To do so, copy the following code block and paste it into Armlab. If you're interested in a high-level overview of what this code block does, a commented version is provided below. &#x20;

{% code overflow="wrap" %}
```bash
{ if [ "$SHELL" != "/bin/bash" ]; then echo "Error: bash is not your login shell"; else \cp /u/cos217/.bash_profile ~/; \cp /u/cos217/.bashrc ~/; \cp /u/cos217/.emacs ~/; \cp /u/cos217/.splintrc ~/; read -p "Enter your name: " name; read -p "Enter your email address: " email; git config --global user.name "$name"; git config --global user.email "$email"; git config --global core.editor emacs; git config --global color.ui auto; exec bash; fi; }
```
{% endcode %}

If you get the message `error: bash is not your login shell`, you must revisit [Activating Your Armlab Account](activating-your-armlab-account.md) and complete step 2. Otherwise, you will be prompted to enter your name and email address. This information will be used for Git configurations.&#x20;

<details>

<summary>Commented Version</summary>

```bash
{
    # If the login shell is not bash, print an error message
    if [ "$SHELL" != "/bin/bash" ]; then
        echo "Error: bash is not your login shell"
    else
        # Copy the .bash_profile file from the /u/cos217/ directory 
        # to the user's home directory (~)
        \cp /u/cos217/.bash_profile ~/

        # Copy the .bashrc file from the /u/cos217/ directory to the 
        # user's home directory (~)
        \cp /u/cos217/.bashrc ~/

        # Copy the .emacs file from the /u/cos217/ directory to the 
        # user's home directory (~)
        \cp /u/cos217/.emacs ~/

        # Copy the .splintrc file from the /u/cos217/ directory to the 
        # user's home directory (~)
        \cp /u/cos217/.splintrc ~/

        # Prompt the user to enter their name, and store it in "name"
        read -p "Enter your name: " name

        # Prompt the user to enter their email address and store it in "email"
        read -p "Enter your email address: " email
        
        # Configure Git with the user's name
        git config --global user.name "$name"

        # Configure Git with the user's email address
        git config --global user.email "$email"

        # Configure Git to use Emacs as the user's default text editor
        git config --global core.editor emacs

        # Configures Git to enable colored output
        git config --global color.ui auto

        # Start a new instance of the Bash shell
        exec bash
    fi
}
```

</details>

