# Automating Builds With make

As we saw in the previous section, managing incremental builds manually is possible but tends to be tedious and error prone. It requires you to:

* Keep track of which files have been modified.
* Understand the dependencies among the files in your program.

Admittedly, for a small program like `testintmath` this might be manageable, but as programs grow larger and the web of dependencies grows increasingly complex, this task becomes incredibly painful to do manually.&#x20;

A much better approach is to automate the process with `make`. To do so, you create a file named `Makefile` or `makefile` in your program's directory, which you populate with a textual representation of your program's [dependency graph](broken-reference). This graph describes the relationships between your program's files and provide make with the necessary build commands. Once you have a suitable Makefile, you can build your program by simply invoking:

```bash
make
```

`make` will read the Makefile and (assuming its set up correctly) build the minimum necessary files to produce an updated executable.
