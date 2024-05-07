# Automating Builds with Make

As we saw in the previous section, managing incremental builds manually can be tedious and error-prone. It requires you to:

* Keep track of which files have been modified.
* Understand the dependencies among the files in your program.

For a small program like `testintmath`, this might be manageable, but as programs grow larger, it becomes increasingly difficult.

A much better approach is to automate the process with 'make'. To do so, you create a file named `Makefile` (or `makefile`) in your program's directory, which you populate with a textual representation of your program's _dependency graph_. Once you have a suitable Makefile, you can build your program by simply invoking:

```bash
make
```

`make` will read the Makefile and (assuming it is set up correctly) build the minimum necessary files to produce an updated executable.
