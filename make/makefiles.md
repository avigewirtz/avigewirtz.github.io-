# Creating a Simple Makefile

As we saw in the previous section, managing incremental builds manually can be tedious and error-prone. It requires you to:

* Keep track of which files have been modified.
* Understand the dependencies among the files in your program.

For a small program like `testintmath`, this might be manageable, but as programs grow larger, it becomes increasingly difficult.

A much better approach is to automate the process with 'make'. To do so, you create a file named `Makefile` (or `makefile`) in your program's directory, which you populate with a dependency graph of the your program. This dependency graph describes the relationships between your program's files and provide 'make' with the necessary build commands. Once you have a suitable Makefile, you can build your program by simply invoking:

```bash
make
```

`make` will read the Makefile and (assuming its set up correctly) build the minimum necessary files to produce an updated executable.

### Dependency Graphs

In such a graph, each file is represented by a node, which, when applicable, is annotated with the commands to build it. Dependencies are indicated by arrows (i.e., directed edges) between nodes. If there is an arrow from file A to file B (A → B), then A depends on B, meaning changes to B require A to be rebuilt. If A → B and B → C, then A is indirectly (or transitively) dependent on C. A change to C requires B to be rebuilt, which in turn requires A to be rebuilt.  A dependency graph for our `testintmath` program is shown in Figure 12.3.&#x20;

<figure><img src="../.gitbook/assets/Group 125 (1).png" alt="" width="563"><figcaption><p>Figure 12.3: testintmath's dependency graph</p></figcaption></figure>

### Describing dependency graoh in text

makefile contain sytanx for rules.

Next, we populate the Makefile with a textual representation of `testintmath`'s dependency graph. This consists of a _dependency rule_ for each object file (`intmath.o`, `testintmath.o`) and for the executable (`testintmath`). A dependency rule has the following syntax:

```
target: dependencies
<tab> command
```

* **Target**: The file you want to build (e.g., `testintmath`).
* **Dependencies**: The files that the target _directly_ depends on (e.g., `intmath.o`, `testintmath.o`).
* **Command**: The command to build the target (e.g., `gcc217 intmath.o testintmath.o -o testintmath`). **Note:** The command must be preceded by a tab.

In our case, we create three dependency rules: one for `testintmath`, one for `testintmath.o`, and one for `intmath.o`. Figuring our which files each of these targets directly depends on can sometimes be challenging, but with our dependency graph, the dependencies are obvious:

* `testintmath` directly depends on `testintmath.o` and `intmath.o`
* `testintmath.o` directly depends on `tetsintmath.c` and `intmath.h`
* `intmath.o` directly depends on `intmath.c` and `intmath.h`

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
