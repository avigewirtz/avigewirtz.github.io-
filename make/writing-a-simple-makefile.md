# Writing a Simple Makefile

Let's now create a makefile for our testintmath program. First, we'll draw a dependency graph for our program. Then, we'll explain how to translate it to make syntax.

#### Constructing a dependency graph

Constructing a dependency graph is quite simple. Let's now create one for our testintmath program.  This can be done by following a few simple steps:

1. Create a node for each of the program  `.c`, `.h`, `.o` files and the executable
2. Draw an arrow from:
   * The executable to each of the `.o` files
   * Each `.o` file to its corresponding `.c` file
   * Each `.o` file to each `.h` file that is `#included` in the `.o` file's corresponding `.c` file
3. Annotate the executable and each object file with the command to build it

This results in the following dependency graph:

<figure><img src="../.gitbook/assets/Group 125 (1).png" alt="" width="563"><figcaption><p>Figure 12.3: testintmath's dependency graph</p></figcaption></figure>

d

The transition from a dependency graph to a makefile is quite straightforward. Let's

We create what is known as a _dependency rule_ for each file in the dependency graph that is not a leaf. In make terminology, such files are called targets. In our case, we have three targets: `intmath.o`, `testintmath.o`, and `testintmath`. Dependency rules have the following syntax:

```
target: dependencies
<tab> command
```

* **Dependencies** . These are the files that the target _directly_ depends on (e.g., `testintmath` directly depends on `testintmath.o` and `intmath.o`). We do not include indirect dependencies.
* **Command**. This is the command make invokes to build the target. Note that it must be preceded by a Tab character.

This results in the following Makefile:

```makefile
testintmath: testintmath.o intmath.o
    gcc217 testintmath.o intmath.o -o testintmath

testintmath.o: testintmath.c intmath.h
    gcc217 -c testintmath.c

intmath.o: intmath.c intmath.h
    gcc217 -c intmath.c
```

### Running our makefile

The general syntax to run a Makefile is:

```bash
make target
```

If you omit a target, `make` defaults to the first target in the makefile.

To build `testintmath`, we can invoke make without specifying a target and make will default to `testintmath`, since it's the first target in our Makefile:

```bash
make
```

If we wanted to build `intmath.o` alone, we'd invoke:

```bash
make intmath.o
```

{% hint style="info" %}
`make` does not read a makefile from top to bottom, processing all rules within it. It starts with the default rule or the rule specified on the command line, and then processes only the rules that are reachable from it.&#x20;
{% endhint %}
