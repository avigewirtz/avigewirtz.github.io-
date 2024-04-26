# makefiles

As we saw in the previous section, managing incremental builds manually is possible but tedious and error-prone. It requires you to:

* Keep track of which files have been modified.
* Understand the dependencies among all the program's files.

A much better approach is to automate the process with `make`. To do this, we create a file in our program's directory known as a Makefile, which we populate with a textual representation of our program's dependency graph. The dependency graph describes the relationships among the files in our program and provides `make` with the commands to build our program.&#x20;

Once we have a suitable Makefile set up, we can run our program by simply invoking:

```bash
make
```

`make` will read the Makefile and build the minimum necessary files required to produce an updated executable.
