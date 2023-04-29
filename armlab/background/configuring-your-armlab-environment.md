# Configuring your armlab environment

The first time you log into armlab, you will need to configure your environment. To do so, copy the following block and paste it into armlab:  &#x20;

{% code overflow="wrap" %}
```bash
[ "$SHELL" != "/bin/bash" ] && { echo "error: bash is not your login shell"; exit 1; }; \cp /u/cos217/.bash_profile /u/cos217/.bashrc /u/cos217/.emacs /u/cos217/.splintrc ~/; read -p "Enter your name: " name; read -p "Enter your email address: " email; git config --global user.name "$name"; git config --global user.email "$email"; git config --global core.editor emacs; git config --global color.ui auto; exec bash
```
{% endcode %}

If you get the message: `error: bash is not your login shell`, you must go back to [Activating Your armlab Account](activating-your-armlab-account.md) and complete step 2. Otherwise, you will be prompted to enter your name and email. This information will be used for Git configurations.&#x20;
