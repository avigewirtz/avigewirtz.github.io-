# Aliases

An alias in Bash is similar to a preprocessor macro in C—it’s a value that Bash expands into something else. You can view the aliases you have set by invoking the `alias` command, which will print all your aliases on stdout:

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

Here, we see that, for example, cp is aliased to cp -i. This means that we invoke cp, we're really invoking cp -i.&#x20;

Aliases have two primary use cases:

* **Shortcut for long command:** If you frequently use a long command, you can create a shorter alias for it. For example, on Armlab, the command `gcc -Wall -Wextra -Wno-unused-parameter -ansi -pedantic` is aliased as `gcc217`. This means you only need to type `gcc217` instead of the entire string of options each time.
* **Changing Default Behavior**: You can also use aliases to modify the default behavior of commands. For example, the command rm deletes a files without prompting for confirmastion.  A common example is `alias rm='rm -i'`, which ensures that by default you're prompted for confirmation before deleting a file.&#x20;

#### Setting Up an Alias

Say you wanted to alias `ll` to `ls -lh`.  If you want the alias to only apply to the current terminal session, you'd use the alias command, like so: &#x20;

```bash
alias ll='ls -lh'
```

To make the alias permanent, you need to add it to your Bash startup file, typically `~/.bashrc`.&#x20;

{% hint style="warning" %}
When you add an alias to your `.bashrc` file, it doesn't take effect until Bash is reloaded. You can reload Bash by starting a new Bash session or by invoking the following command:&#x20;

```bash
source ~/.bashrc
```
{% endhint %}

#### Avoiding Alias Expansion

To avoid alias expansion, you can prefix the command with a backslash. For example, if `ls` is aliased to `ls --color=always` (as is the case on Armlab), you can run `\ls` to execute the original `ls` command without any options.
