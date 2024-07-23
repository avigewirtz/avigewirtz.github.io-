# Writing a Simple Makefile

Assume the working directory contains `testintmath`'s source files (i.e., `testintmath.c`, `intmath.c`, and `intmath.h`). To build `testintmath` with `make`, the first step is to create a makefile in the working directory. You can name the makefile whatever you like, but `make` automatically searches for a file named `makefile` or `Makefile`, making these names more convenient. You can create the Makefile by running the following command:

```bash
touch Makefile
```

The next step is to populate the Makefile with `testintmath`'s dependency graph. As we mentioned earlier, a dependency graph is a directed graph that contains two pieces of information:

* The dependencies between the source files, object files, and the executable.
* The commands to build each file from its dependencies.

Visually, it looks like this:

<figure><img src="../.gitbook/assets/Frame 33.png" alt="" width="563"><figcaption></figcaption></figure>

The interpretation of this graph should hopefully be self-explanatory.&#x20;

* Arrows indicate dependencies, pointing from a file to what it depends on.
* Each file with dependencies is labeled with the command to build it from its dependencies. In `make` terminology, these files are known as _targets_. They correspond to object files and the executable.&#x20;

The neat thing about dependency graphs is they make it extremely easy to see which files are rendered obsolete by changes to one or more of the source files. Just follow the arrows. Any file which directly or indirectly points to the modified source files is rendered obsolete. For example, if `intmath.c` is modified, `intmath.o` and `testintmath` are rendered obsolete, but `testintmath.o` is not.

Translating this dependency graph into a Makefile is remarkably straightforward. We create a _dependency rule_ for each target in the dependency graph. Dependency rules have the following syntax:

```makefile
target: direct_dependencies
<tab> command
```



*
*
* Our dependency graph has three targets: the executable `testintmath`, and the object files `testintmath.o` and `intmath.o`. This results in a makefile with three rules. Here is the complete Makefile:
*

```makefile
testintmath: testintmath.o intmath.o
    gcc testintmath.o intmath.o -o testintmath

testintmath.o: testintmath.c intmath.h
    gcc -c testintmath.c

intmath.o: intmath.c intmath.h
    gcc -c intmath.c
```

Notice how this Makefile is nothing more than a textual representation of the dependency graph we showed above. That is the core of `make`. A language for specifying and interpreting dependency graphs.

*
