# Bash Shortcuts

Bash offers many useful command-line shortcuts that minimize the need to type out long commands. We've already seen two shortcuts: tilde expansion and Tab completion. Here, we'll cover three more: Aliases, command history, and wildcards.&#x20;

### History

Bash keeps a record of the commands you've entered in a file named `.bash_history`, typically stored in your home directory. You can view This allows you to perform a few extremely useful operations:&#x20;

* **Display your command history:**  Invoke `history`.&#x20;
* **Search your command history**: Press`Ctrl-r` and type a few characters of the command you're looking for. Press `Ctrl-r` again to cycle through matching commands.
* **Navigate your command history**: Use the up and down arrow keys.
* **Reuse commands**: Use the `!` (bang) operator followed by a number (e.g., `!125`), to execute the command with that number in the history.&#x20;

### Aliases

An alias in Bash is similar to a preprocessor macro in C—it’s a value that Bash expands into something else. It has two primary use cases:

* **Shortcut for long command:** If you frequently use a long command, you can create a shorter alias for it. For example, on Armlab, the command `gcc -Wall -Wextra -Wno-unused-parameter -ansi -pedantic` is aliased as `gcc217`. This means you only need to type `gcc217` instead of the entire string of options each time.
* **Changing Default Behavior**: You can also use aliases to modify the default behavior of commands. A common example is `alias rm='rm -i'`, which makes the `rm` command interactive, prompting you for confirmation before deleting files.

#### Viewing aliases

You can view the aliases you have set by invoking the `alias` command, which will print all your aliases on stdout:

```bash
~> alias
alias cp='cp -i'
alias egrep='egrep --color=auto'
alias fgrep='fgrep --color=auto'
alias gcc217='gcc -Wall -Wextra -Wno-unused-parameter -ansi -pedantic'
alias grep='grep --color=auto'
alias less='less --quit-at-eof --no-init --tabs=4 --RAW-CONTROL-CHARS'
alias ln='ln -i'
alias ls='ls -a --color=always'
alias mv='mv -i'
alias mysql='mysql -u root -p'
alias rm='rm -i'
~> 
```

#### Setting an Alias

To set an alias temporarily, use the `alias` command. For example, to set `ll` as an alias for `ls -lh`, you would run:

```bash
alias ll='ls -lh'
```

This alias lasts until the terminal session ends. To make an alias permanent, you need to add it to your Bash startup file, typically `~/.bashrc`.&#x20;

{% hint style="warning" %}
When you add an alias to your `.bashrc` file, it doesn't take effect until you start a new Bash session. To make the alias available immediately, you can activate it by running the following command:

```bash
source ~/.bashrc
```
{% endhint %}

### **Wildcards**

Wildcards are characters that can represent any number of characters or a specific range of characters in a pattern. They are helpful when you need to perform an operation on multiple files or directories that share a similar naming pattern. Two commonly used wildcards in Bash are:

* `*` (asterisk): This represents any number of characters (including zero characters). For example, `*.txt` will match any file that ends with the `.txt` extension in the current directory, such as `notes.txt`, `chapter1.txt`, and `todo.txt`.&#x20;
* `?` (question mark): This represents exactly one character. For example, `file?.txt` matches with files like `file1.txt`, `file2.txt`, but not `file12.txt`.
