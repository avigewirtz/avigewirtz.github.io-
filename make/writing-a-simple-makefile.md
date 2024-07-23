# Writing a Simple Makefile

Assume the working directory contains `testintmath`'s source files (i.e., `testintmath.c`, `intmath.c`, and `intmath.h`). To build `testintmath` with `make`, the first step is to create a makefile in the working directory. You can name the makefile whatever you like, but `make` automatically searches for a file named `makefile` or `Makefile`, making these names more convenient. To create the makefile, run the following command:

```bash
touch Makefile
```

The next step is to populate the Makefile `testintmath`'s dependency graph. As we mentioned earlier, a dependency graph is a directed graph that contains two pieces of information:

* The dependencies between the source files, object files, and the executable.
* The commands to build each file from its dependencies.

Visually, it looks like this:

<figure><img src="../.gitbook/assets/Frame 33.png" alt="" width="563"><figcaption></figcaption></figure>

This graph tells us the following:

* `testintmath` depends on `testintmath.o` and `intmath.o`, and the command to build `testintmath` is `gcc testintmath.o intmath.o -o testintmath.`
* `testintmath.o` depends on `testintmath.c` and `intmath.h`, and the command to build `testintmath.c` is `gcc -c testintmath.c`.
* `intmath.o` depends on `intmath.c` and `intmath.h`, and the command to build `intmath.c` is `gcc -c intmath.c`.

Each node represents a file is represented by a The nodes represent filesAn arrow from file A to B indicates that file A depends on B. For example, the we see that `intmath.o` depends on `intmath.c` and `intmath.h`. Each file with dependencies is labeled with the command to build it. In make terminology, these files are known as _targets_.

The neat thing about dependency graphs is they make it really easy to see which files are rendered obsolete by changes to one of the source files. Just follow the arrows. Any file which directly or indirectly points to the modified source file is rendered obsolete. For example, if intmath.c is modified, intmath.o and testintmath are rendered obsolete.

There is a difference, however, between direct and transitive dependencies. For example, `intmath.o` directly depends on `intmath.c`, but `testintmath` only transitively depends on `intmath.c`.

{% hint style="info" %}
Note that we're not including the header files `stdio.h` and `stdlib.h` in the dependency graph, even though `testintmath.c` #includes them, since these ar system header files that we don't modify. As such, don't need to be concerned with them in Makefiles.
{% endhint %}

Translating this dependency graph into a Makefile is remarkably straightforward. We create a _target rule_ for each target in the dependency graph. The rule soecifies which files the target directly depends on and the command to build the target. it's syntax is as follows:

```makefile
target: direct_dependencies
<tab> command
```

The interpretation of this dependency graph should hopefully be pretty self-explanatory.

*

Note the tab character on the second line preceding the command.

Our dependency graph has three targets: the executable `testintmath`, and the object files `testintmath.o` and `intmath.o`. This results in a makefile with three rules. Here is the complete Makefile:

```makefile
testintmath: testintmath.o intmath.o
    gcc testintmath.o intmath.o -o testintmath

testintmath.o: testintmath.c intmath.h
    gcc -c testintmath.c

intmath.o: intmath.c intmath.h
    gcc -c intmath.c
```

Notice how this Makefile is nothing more than a textual representation of the dependency graph we showed above. That is the core of `make`. A language for specifying and interpreting dependency graphs.
