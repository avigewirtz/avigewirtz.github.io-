# Ignoring Files

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
