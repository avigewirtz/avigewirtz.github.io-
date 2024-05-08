# Creating a Simple Makefile

As we saw in the previous section, managing incremental builds manually is possible but tends to be tedious and error prone. It requires you to:

* Keep track of which files have been modified.
* Understand the dependencies among the files in your program.

Admittedly, for a small program like `testintmath` this might be manageable, but as programs grow larger, it becomes increasingly difficult.

A much better approach is to automate the process with 'make'. To do so, you create a file named `Makefile` (or `makefile`) in your program's directory, which you populate with a textual representation of your program's _dependency graph_ (see below). This graph describes the relationships between your program's files and provide make with the necessary build commands. Once you have a suitable Makefile, you can build your program by simply invoking:

```bash
make
```

`make` will read the Makefile and (assuming its set up correctly) build the minimum necessary files to produce an updated executable.

### Dependency Graphs

A program's dependencies can be formally described with what is known as a _dependency graph_. A dependency graph for our `testintmath` program is shown in Figure 12.3.&#x20;

<figure><img src="../.gitbook/assets/Group 125 (1).png" alt="" width="563"><figcaption><p>Figure 12.3: testintmath's dependency graph</p></figcaption></figure>

### Dependency Rules

The transition from a dependency graph to a makefile is quite straightforward. We create a what is known as a dependency rule for each file that is created via a build. In make terminology, such files are called targets. Targets are easy to identify, since they correspond to leaf nodes (i.e., nodes with no children). In our case, we have three targets: `intmath.o`, `testintmath.o`, and `testintmath`. Dependency rules have the following syntax:

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
