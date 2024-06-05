# Aliases

Suppose you frequently use the following long command to build your C programs:

An alias in `bash` is similar to a preprocessor macro in C—it’s a value that `bash` expands into something else. They allows you to replace a command with another string that Bash expands when you execute the command. You can view all the aliases you have set by running the `alias` command:

Repeatedly typing this command gets annoying quickly. To make life easier, you can alias it to something shorter, such as gcc217. To do so, you’d add the following line to your .bashrc file:

gcc217=‘gcc -Wall -Wextra -Wno-unused-parameter -ansi -pedantic’

Going forward, instead of typing out the long command, you simply type gcc217, and bash will replace it with gcc -Wall -Wextra -Wno-unused-parameter -ansi -pedantic. Note, however, that by default, this alias will not take effect until your next Bash session. To make it take effect immediately, you can run the following command:

If you want the alias to only apply to the current terminal session, you'd use the alias command, like so:

Here, we see that, for example, cp is aliased to cp -i. This means that we invoke cp, we're really invoking cp -i.&#x20;

```bash
alias ll='ls -lh'
```

Another common use case of aliases is to change the default behavior of a command. Consider the rm command. By default, it deletes non-empty files and directories without prompting the user for confirmation. A common practice is to alias rm to rm -i, which changes the default behavior of rm to prompt for confirmation.

#### Setting an Alias

Say you wanted to alias `ll` to `ls -lh`. Explain that this does. If you want the alias to only apply to the current terminal session, you'd use the alias command, like so: &#x20;

#### Viewing Your Aliases

You can view the aliases you have set by invoking the `alias` command. On my PC, I get the following output:

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

#### Avoiding Alias Expansion

To avoid alias expansion, you can prefix the command with a backslash. For example, if `ls` is aliased to `ls --color=always` (as is the case on Armlab), you can run `\ls` to execute the original `ls` command without any options.

#### Removing an Alias

To remove an alias, type
