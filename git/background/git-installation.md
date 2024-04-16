# First time Git setup

1.  **Set your name**: This command configures Git with your username, which is used to identify the author of commits.

    ```bash
    git config --global user.name "YOUR_NAME"
    ```

    Replace `YOUR_NAME` with your actual name. This name will appear in your commits and in the history of your projects. Example:

    ```bash
    git config --global user.name "John Smith"
    ```
2.  **Set your email address**: This command sets the email address that will be associated with your Git commits.

    ```bash
    it config --global user.email YOUR_EMAIL_ADDRESS
    ```

    Replace `YOUR_EMAIL_ADDRESS` with your email. This should be the same email associated with your GitHub account if you plan to push to GitHub repositories. Example:

    ```bash
    bashCopy codegit config --global user.email johnsmith@gmail.com
    ```
3.  **Set your preferred text editor**: This command specifies which text editor Git will open for things like commit messages:&#x20;

    ```bash
    bashCopy codegit config --global core.editor NAME_OF_PREFERRED_EDITOR
    ```

    Replace `NAME_OF_PREFERRED_EDITOR` with the command that launches your preferred editor. This setting depends on the editor you like to use (e.g., vim, emacs, nano). Example:

    ```bash
    git config --global core.editor emacs
    ```
4.  **Change the default branch name to "main"**: This command sets "main" as the default branch name for all new repositories you initialize on your system. This is useful as many projects have moved away from using "master" as the default branch name.

    ```bash
    git config --global init.defaultBranch main
    ```

