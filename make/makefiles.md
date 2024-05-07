# Creating a Simple Makefile

As we saw in the previous section, managing incremental builds manually can be tedious and error-prone. It requires you to:

* Keep track of which files have been modified.
* Understand the dependencies among the files in your program.

For a small program like `testintmath`, this might be manageable, but as programs grow larger, it becomes increasingly difficult.

A much better approach is to automate the process with 'make'. To do so, you create a file named `Makefile` (or `makefile`) in your program's directory, which you populate with a _dependency graph_ of the your program. Such a graph describes the relationships between your program's files and provide 'make' with the necessary build commands. Once you have a suitable Makefile, you can build your program by simply invoking:

```bash
make
```

`make` will read the Makefile and (assuming its set up correctly) build the minimum necessary files to produce an updated executable.

### Dependency Graphs

The dependencies among files in a program can be formally described with a dependency graph. In such a graph, each node represents a file. When applicable, the node is labeled with the command to build it. A directed edge (arrow) from A to B (A -> B) indicates that file A depends on file B, meaning that changes to B require A to be rebuilt. If A → B and B → C, then A is indirectly (or transitively) dependent on C. A change to C requires B to be rebuilt, which in turn requires A to be rebuilt. A dependency graph for our `testintmath` program is shown in Figure 12.3.&#x20;

<figure><img src="../.gitbook/assets/Group 125 (1).png" alt="" width="563"><figcaption><p>Figure 12.3: testintmath's dependency graph</p></figcaption></figure>

### Describing dependency graph in text

Each node that isn't a leaf is known as a target in make terminology. Create a rule for each target.&#x20;

```
target: dependencies
<tab> command
```

* **Target**: The file you want to build.&#x20;
* **Dependencies**: The files that the target depends on. Note that you do not list indirect dependencies here.
* **Command**: The command to build the target. **Note:** The command must be preceded by a tab.

This results in the following makefile:

```makefile
testintmath: testintmath.o intmath.o
    gcc217 testintmath.o intmath.o -o testintmath

testintmath.o: testintmath.c intmath.h
    gcc217 -c testintmath.c

intmath.o: intmath.c intmath.h
    gcc217 -c intmath.c
```

### Running our makefile

The general syntax to run a makefile is:

```bash
make target
```

If you omit a target, `make` defaults to the first target in the makefile.&#x20;

To build `testintmath`, we can invoke `make` without arguments and it'll default to `testintmath`, since `testintmath` is the first target in our makefile:

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
