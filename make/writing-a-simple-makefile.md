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

Interpreting this graph is straightforward:

* Arrows indicate dependencies, pointing from a file to the files it depends on. We see that `testintmath` depends on `testintmath.o` and `intmath.o`, which in turn depend on their corresponding source files (`testintmath.c` and `intmath.c`) and the common header file `intmath.h`.
* Each file with dependencies is labeled with the command to build it from its dependencies. In `make` terminology, these files are known as _targets_. Our dependency graph has three targets: `testintmath`, `testintmath.o` and `intmath.o`. As a general rule, targets typically correspond to binary files.

The neat thing about dependency graphs is they make it extremely easy to see which files are rendered obsolete by changes to one or more of the source files. Just follow the arrows. Any file which directly or indirectly points to the modified source files is rendered obsolete. For example, if `intmath.c` is modified, we see that `intmath.o` and `testintmath` are rendered obsolete, but `testintmath.o` is not.

Translating this dependency graph into a Makefile is remarkably straightforward. We create a _dependency rule_ for each target in the dependency graph. Dependency rules have the following syntax:

```makefile
target: dependencies
<tab> command
```

This syntax should hopefully be self-explanatory, but note a couple of things:

* `dependencies` refers to direct dependencies, not transitive dependencies.
* The command must be preceded by a tab character (and not spaces). Failure to do so will result in the following error: `*** missing separator. Stop.`

Here is the complete Makefile for our program:

```makefile
testintmath: testintmath.o intmath.o
    gcc testintmath.o intmath.o -o testintmath

testintmath.o: testintmath.c intmath.h
    gcc -c testintmath.c

intmath.o: intmath.c intmath.h
    gcc -c intmath.c
```

#### Running make

With the Makefile set up, you can now build `testintmath` using `make`. The basic syntax to run make is:

```makefile
make target
```

where `target` is the name of the file you want `make` to build (see, however, [phony targets](makefile-version-2-phony-targets.md)). If you omit a target, make defaults to the first target in the Makefile, which in our case is `testintmath`. Therefore, you can build `testintmath` by simply running:

```bash
make
```

If `testintmath` is already up-to-date, make will report that fact and halt. Otherwise, it will execute the necessary commands to bring `testintmath` up-to-date. By default, `make` prints the commands it executes on stdout. Let's examine the behavior of `make` with our newly created Makefile.&#x20;

Assume we're building `testintmath` for the first time. Running make, you should see the following output:

```bash
$ make
gcc -c testintmath.c
gcc -c intmath.c
gcc testintmath.o intmath.o -o testintmath
$
```

Observe that `make` compiles both source files into object files, then links them to create the `testintmath` executable. Now, let's run `make` again immediately afterward:

```bash
$ make
make: 'testintmath' is up to date.
$
```

`make` determines that no files have been modified since the last build, so no action is necessary.

Next, let's "modify" `intmath.c`. The `touch` command updates the file's "last modified" timestamp without changing its contents. This simulates the effect of editing and saving the file.

```bash
$ touch intmath.c
```

Running make:

```bash
$ make
gcc -c intmath.c
gcc testintmath.o intmath.o -o testintmath
$
```

Observe that `make` only recompiles `intmath.c` and relinks the executable. It doesn't recompile `testintmath.c` as it hasn't been modified.

Now, let's simulate a change to the header file:

```bash
$ touch intmath.h
$ make
gcc -c testintmath.c
gcc -c intmath.c
gcc testintmath.o intmath.o -o testintmath
$
```

In this case, `make` recompiles both source files. This is because both include `intmath.h`, so changes to the header file necessitate recompilation of all dependent source files.
