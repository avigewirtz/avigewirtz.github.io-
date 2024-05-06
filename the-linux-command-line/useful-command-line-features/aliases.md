# Aliases

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
