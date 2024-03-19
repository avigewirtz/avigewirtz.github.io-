# Useful Command-line Features

Bash offers many useful command-line shortcuts that minimize the need to type out long commands, filenames, or pathnames. Some common shortcuts include:

### **Tilde Expansion**

The tilde (\~) character expands into your user's home directory. For example, if your username is `your_NetID`, and your home directory is `/u/your_NetID`,  `~` will expand to `/u/your_NetID`.

### **TAB Completion**

When you type a partial command or pathname and press the TAB key, Bash will attempt to autocomplete the text. For example, if you type `pw TAB`, you might get something like this:

```bash
> pw
pwd  pwd_mkdb  pwpolicy  
> pw
```

### **Command History**

Bash keeps a record of the commands you've entered in a file named `.bash_history`, typically stored in your home directory. You can view This allows you to perform a few extremely useful operations:&#x20;

* **Display your command history:**  Invoke `history`.&#x20;
* **Search your command history**: Press`Ctrl-r` and type a few characters of the command you're looking for. Press `Ctrl-r` again to cycle through matching commands.
* **Navigate your command history**: Use the up and down arrow keys.
* **Reuse commands**: Use the `!` (bang) operator followed by a number (e.g., `!125`), to execute the command with that number in the history.&#x20;
* **Clearing terminal window**: Invoke `clear` command or press `Ctrl-l`. This clears your terminal screen of all visible content. &#x20;

### **Aliases**

Say you get tired of typing a long command, such as

* couple of uses cases
  * long command
  * changing default behavior

An alias is a user-defined string that serves as a shortcut for a longer command or a sequence of commands. Aliases must be the first word in a command. You can view the aliases you have set by invoking alias. Here's an example:

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

### **Wildcards**

Wildcards are characters that can represent any number of characters or a specific range of characters in a pattern. They are helpful when you need to perform an operation on multiple files or directories that share a similar naming pattern. The two most commonly used wildcards in Bash are:

* `*` (asterisk): Represents any number of characters (including zero characters). For example, `*.txt` matches all .txt files in the current directory.&#x20;
* `?` (question mark): Represents exactly one character. For example, `file?.txt` matches files like `file1.txt`, `file2.txt`, but not `file12.txt`.

\
\
