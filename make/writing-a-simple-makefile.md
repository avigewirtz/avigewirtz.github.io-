# Writing a Simple Makefile

Assume the working directory contains `testintmath`'s source files (i.e., `testintmath.c`, `intmath.c`, and `intmath.h`). To build `testintmath` with `make`, the first step is to create a makefile in the working directory. You can name the makefile whatever you like, but `make` automatically searches for a file named `makefile` or `Makefile`, making these names more convenient.&#x20;

Once you have created a Makefile, the next step is to populate it with `testintmath`'s dependency graph. As we mentioned earlier, a dependency graph is a directed graph that contains two pieces of information:

* The dependencies between the source files, object files, and the executable.
* The commands to build each file from its dependencies.

Visually, it looks like this:

<figure><img src="../.gitbook/assets/Frame 33.png" alt="" width="563"><figcaption></figcaption></figure>

Interpreting this graph is straightforward:

* Arrows indicate dependencies, pointing from a file to the files it depends on. We see that `testintmath` depends on `testintmath.o` and `intmath.o`, which in turn depend on their corresponding source files (`testintmath.c` and `intmath.c`) and the common header file `intmath.h`.
* Each file with dependencies is labeled with the command to build it from its dependencies. In `make` terminology, these files are known as _targets_. Our dependency graph has three targets: `testintmath`, `testintmath.o` and `intmath.o`. For convenience, these targets are circled in red. As a general rule, targets correspond to binary files.

The neat thing about dependency graphs is they make it extremely easy to see which files are rendered obsolete by changes to one or more of the source files. Just follow the arrows. Any file that directly or indirectly points to the modified source files is rendered obsolete. For example, if `intmath.c` is modified, we see that `intmath.o` and `testintmath` are rendered obsolete (but `testintmath.o` is not).

Translating this dependency graph into a Makefile is remarkably straightforward. We create a _dependency rule_ for each target in the dependency graph. Dependency rules have the following syntax:

```makefile
target: dependencies.
<tab> command
```

This syntax should hopefully be pretty self-explanatory, but note a couple of things:

* `dependencies` refers to _direct_ dependencies, not transitive dependencies (dependencies that exist through intermediate files in the dependency graph). In our case, `testintmath` directly depends on the object files but only transitively depends on the source files. Therefore, we list only the object files as dependencies of `testintmath`. The source files will be listed in the rules for the object files.
* The command must be preceded by a tab character (and not spaces). Failure to do so will result in the following error: `*** missing separator. Stop.`

Here is the complete Makefile for our program, containing three rules:

```makefile
testintmath: testintmath.o intmath.o
    gcc testintmath.o intmath.o -o testintmath

testintmath.o: testintmath.c intmath.h
    gcc -c testintmath.c

intmath.o: intmath.c intmath.h
    gcc -c intmath.c
```

The first rule declares that testintmath depends on tetsintmath.o and intmath.o and that the command to build testintmath is gcc testintmath.o intmath.o -o testintmath. The next two rules give analogous information for tetsintmath.o and intmath.o.&#x20;

Notice how this Makefile is nothing more than a textual representation of the dependency graph shown above. With this Makefile set up, you can now build `testintmath` using `make`. &#x20;
