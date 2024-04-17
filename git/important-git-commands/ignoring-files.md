# Ignoring Files

While you’re working on a project, you may have files in your working directory that you want Git to simply ignore. If it’s a small project in an interpreted language, this may not happen so much, but it’s definitely an issue for projects that produce compiled code of any sort, or use tools like autoconf, or generate documentation automatically in various formats. Such files include:



object code\
\*.o, \*.so, \*.a, \*.dll, \*.exe

bytecode\
\*.jar (Java), \*.elc (Emacs Lisp), \*.pyc (Python)

toolchain artifacts\
config.log, config.status, aclocal.m4, Makefile.in, config.h

Generally speaking, anything that is automatically generated you probably don’t want tracked by Git, and you don’t want Git con‐ stantly including them in listings or complaining about them ei‐ ther. Git looks at three different kinds of files to determine what to ignore, in order:

1. Files named .gitignore in your working tree. This is just another file to Git as far as content is concerned—it will list it as “untracked” if it’s present but not in the repository— and so you normally add it to the repository content; thus, if this is shared work, you should only put things there that make sense for other people to ignore as well. You can ac‐ tually put .gitignore in a .gitignore file, and cause it to ignore itself. All .gitignore files in the current and contain‐ ing directories in the repository are read, with rules in files closer to the current directory overriding those in files far‐ ther away.
2. The per-repository file .git/info/exclude. This is part of your repository configuration, but not part of the repository content, so unlike a tracked .gitignore file, it is not auto‐ matically foisted upon people who clone your project. This is a good place to put things you find convenient to ignore for this project, but about which others might disagree (or if you simply decide not to use .gitignore files as a matter of policy, to avoid confusion).
3.  A file named by the configuration variable core.excludes file, if you set it. You might do this:

    ```
          $ git config --global core.excludesfile ~/.gitignore
    ```

Ignoring Files | 43

and keep a set of ignore patterns there that you want Git to always observe. That’s assuming your home directory is not itself inside a Git repository, of course, in which case you might want to name the file something else (and ask yourself if you don’t perhaps like Git just a bit too much).









Sometimes you want Git to ignore certain files from the worktree. For example, in the Decomment assignment, your worktree will contain these four files, generated from preprocessing, compiling, assembling, and linking:&#x20;

* _decomment.i_: Preprocessed output
* _decomment.s_: Assembly code
* _decomment.o_: Object file
* _decomment_: Executable file

Because these files are not part of the source code, you may not want to include them in your Git repository.&#x20;

You can tell Git not to ignore them by adding them to the ._gitignore_ file. The _.gitignore_ file in such a case may have the following structure:&#x20;

```txt
# Ignore object files
*.o

# Ignore assembly files
*.s

# Ignore preprocessed output
*.i

# Ignore executable files
decomment
```
