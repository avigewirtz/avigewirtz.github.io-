# Configuring your armlab environment

The first time you log into armlab, you will need to configure your environment. To do so, copy the following block and paste it into armlab:  &#x20;

{% code overflow="wrap" %}
```bash
[ "$SHELL" != "/bin/bash" ] && { echo "error: bash is not your login shell"; exit 1; }; \cp /u/cos217/.bash_profile /u/cos217/.bashrc /u/cos217/.emacs /u/cos217/.splintrc ~/; read -p "Enter your name: " name; read -p "Enter your email address: " email; git config --global user.name "$name"; git config --global user.email "$email"; git config --global core.editor emacs; git config --global color.ui auto; exec bash
```
{% endcode %}

If you get the message: `error: bash is not your login shell`, you must revisit [Activating Your armlab Account](activating-your-armlab-account.md) and complete step 2. If your shell is configured correctly, you will be prompted to enter your name and email address. This information will be used for Git configurations.&#x20;

Here's a breakdown of each command in the given code block:

1. Check if the current shell is not Bash:

    ```bash
    [ "$SHELL" != "/bin/bash" ]
    ```

2. Use logical AND operator to execute following commands if previous condition is true:

    ```bash
    &&
    ```

3. Display an error message and exit the script if the current shell is not Bash:

    ```bash
    { 
        echo "error: bash is not your login shell"; 
        exit 1; 
    }
    ```

4. Copy configuration files from a specific directory to the user's home directory:

    ```bash
    \cp /u/cos217/.bash_profile /u/cos217/.bashrc /u/cos217/.emacs /u/cos217/.splintrc ~/
    ```

5. Prompt the user to enter their name and store it in a variable:

    ```bash
    read -p "Enter your name: " name
    ```

6. Prompt the user to enter their email address and store it in a variable:

    ```bash
    read -p "Enter your email address: " email
    ```

7. Set the user's name for Git configuration using the previously entered value:

    ```bash
    git config --global user.name "$name"
    ```

8. Set the user's email address for Git configuration using the previously entered value:

    ```bash
    git config --global user.email "$email"
    ```

9. Set Emacs as the default text editor for Git:

    ```bash
    git config --global core.editor emacs
    ```

10. Enable automatic colorization of Git output in the terminal:

    ```bash
    git config --global color.ui auto
    ```

11. Replace the current shell with a new instance of Bash to reload the shell and apply the updated configurations:

    ```bash
    exec bash
    ```
