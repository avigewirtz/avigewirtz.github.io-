# First time Git setup

Git will guess your name and email address from the environ‐ ment, but those may vary from one computer to another and may not be what you want. To set them:

```
    $ git config --global user.name "Richard E. Silverman"
    $ git config --global user.email res@oreilly.com
```



When you use git commit, you supply some free-form text, which is included in the commit; this is the “commit message.” You can give this on the command line with the -m switch, but you can also use your favorite text editor to compose the message instead. If you omit the -m switch, Git starts a text editor to let you write your message. The default editor varies by platform; on Unix, it is the ubiquitous vi. You can customize this with the environment variables GIT\_EDITOR, EDITOR, or VISUAL (the latter two are re‐ spected by many other Unix programs as well), or by setting core.editor. For example (reflecting the author’s predilections):

```
    $ git config --global core.editor emacs
```

Git uses the first of these variables it finds in the order given.







Color

Many Git commands, including diff, log, and branch, can use color to help you interpret their output, but these options are mostly off by default. To enable the use of color generally, set:

```
    $ git config --global color.ui auto
```

(ui stands for “user interface.”) This will turn on most color op‐ tions when Git is talking to a terminal (tty/pty device). You can then turn off color for individual commands if you prefer; for example, to disable it for git branch (but leave it on for other functions):

```
    $ git config --global color.branch no
```

Git’s use of color is very configurable, down to defining new color names, specifying terminal control sequences, and using color in custom log formats. See git-config(1) and git-log(1) for details.

















**Set your name**: This command configures Git with your username, which is used to identify the author of commits.

```bash
git config --global user.name "YOUR_NAME"
```

Replace `YOUR_NAME` with your actual name. This name will appear in your commits and in the history of your projects. Example:

```bash
git config --global user.name "John Smith"
```

1.  **Set your email address**: This command sets the email address that will be associated with your Git commits.

    ```bash
    it config --global user.email YOUR_EMAIL_ADDRESS
    ```

    Replace `YOUR_EMAIL_ADDRESS` with your email. This should be the same email associated with your GitHub account if you plan to push to GitHub repositories. Your name and email address were configured automatically based

    on your username and hostname..
2. Example:

```bash
bashCopy codegit config --global user.email johnsmith@gmail.com
```

1.  **Set your preferred text editor**: This command specifies which text editor Git will open for things like commit messages:&#x20;

    ```bash
    bashCopy codegit config --global core.editor NAME_OF_PREFERRED_EDITOR
    ```

    Replace `NAME_OF_PREFERRED_EDITOR` with the command that launches your preferred editor. This setting depends on the editor you like to use (e.g., vim, emacs, nano). Example:

    ```bash
    git config --global core.editor emacs
    ```
2.  **Change the default branch name to "main"**: This command sets "main" as the default branch name for all new repositories you initialize on your system. This is useful as many projects have moved away from using "master" as the default branch name.

    ```bash
    git config --global init.defaultBranch main
    ```

