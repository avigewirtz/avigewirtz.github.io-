# Automating Builds With make

To automate builds with `make`, you create a file named `Makefile` (or `makefile`) in your program's directory. In this Makefile, you describe the dependencies between the files in your program and provide `make` with the necessary commands to build each file from its dependencies. Once you have a suitable Makefile set up, you can build your entire program by simply invoking:

```bash
make
```

`make` will read the Makefile, and, assuming it is set up correctly, build the minimum necessary files to produce an updated executable.&#x20;

### Dependency Graphs

The dependencies among the files in a program can be formally described via a _dependency graph_. In this graph, nodes represent files, and directed edges indicate dependencies. If file A -> B, then A depends on B, meaning that a modification to B requires A to be rebuilt. If A -> B and B -> C, then A indirectly (or transitively) depends on C. A modification to C requires B to be rebuilt, which in turn requires A to be rebuilt. Each file with dependencies is labeled with the command to build it from its dependencies. In make terminology, these files are known as targets. A visual representation of our program's dependency graph is shown in Figure 12.3.

<figure><img src="../.gitbook/assets/Group 125 (1).png" alt="" width="563"><figcaption><p>Figure 12.3: testintmath's dependency graph</p></figcaption></figure>

Notice a few characteristics of our dependency graph. These are common among C programs.&#x20;

* 2 levels of dependencies. Execuitable object file depends on relocateable object files, and relocateable object files depend on .c and .h files.&#x20;
* `.c` and `.h` files do not have any dependencies. This makes sense, since source files are not "built".
* one-to-one relationship between .c and .o files.&#x20;
* many-to-many relationship between .h and .o files.

#### Dependency Graph to Makefile


The transition from a dependency graph to a makefile is quite straightforward. 


We create what is known as a _dependency rule_ for each target in the dependency graph. In our case, that corresponds to testintmath.o, intmath.o, and testintmath. Dependency rules have the following syntax:

```
target: dependencies
<tab> command
```

* **Dependencies** . These are the files that the target depends on (e.g., `testintmath` depends on `testintmath.o` and `intmath.o`). 

* **Command**. This is the command to build the target. In our graph, each target is labeled with the command to build it. Note that the command must be preceded by a Tab character.

This results in three dependency rules: one for testintmath, one for intmath.o, and one for testintmath.o, leading to the following makefile:

```makefile
testintmath: testintmath.o intmath.o
    gcc217 testintmath.o intmath.o -o testintmath

testintmath.o: testintmath.c intmath.h
    gcc217 -c testintmath.c

intmath.o: intmath.c intmath.h
    gcc217 -c intmath.c
```

### Running a makefile

The general syntax to run a Makefile is:

```bash
make target
```
 Where `target` is the name of the file you want `make` to build. For example, to build `intmath.o`, you'd invoke:


```bash
make intmath.o
```

If you omit a target, `make` defaults to the first target in the Makefile. In our Makefile, testintmath is the first target. Thus, invoking:

```bash
make
```
Is equivalent to invoking:

```bash
make testintmath
```
In both cases, make will build testintmath. 

{% hint style="info" %}
`make` does not read a makefile from top to bottom, processing all rules within it. It starts with the first rule or the rule specified on the command line, and then processes only the rules that are reachable from it.&#x20;
{% endhint %}
