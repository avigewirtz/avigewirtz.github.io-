# Makefiles

As we saw in the previous section, managing incremental builds manually is possible but it requires you to:

* Keep track of which files have been modified.
* Have a good grasp the dependencies among the files in the program.&#x20;

For a small program like `testintmath`, this task isn't too bad. But as programs grow in size and the web of dependencies becomes more and more complex, rebuilding programs manually becomes extremely tedious and error prone.

A much better approach is to automate the process with `make`. To do this, we create a file in our program's directory known as a _Makefile_, in which we describe the dependencies of among the files in our program and provides `make` with the commands to build them. The Makefile can be named `Makefile`, `makefile`, or even `GNUmakefile` (assuming you're using GNU Make). GNU recommends `Makefile`. Once we have a appropriate Makefile set up, we can run our program by simply invoking:

```bash
make
```

`make` will read the Makefile and (assuming our makefile is set up correctly) build the minimum necessary files to produce an updated executable.
