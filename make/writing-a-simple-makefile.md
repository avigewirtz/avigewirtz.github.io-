# Writing a Simple Makefile

* Continuing with our testintmath example, we'll show to use make to build our program.

* Assume the working directory contains the files of our testintmath program. When you run make, make looks for a file in the working directory named makefile or Makefile. Thus, our first step is to create such a file. I personally prefer Makefile, since it makes it stand out more, but either option is good. 

```
touch Makefile
```




named Makefile or makefile. (In practice, the makefile can be named something other than Makefile or makefile, but then you'd need to specify its name on the command line when you run make.)
* The next step is to populate the Makefile with a dependency graph for testintmath. before we show how to write the dependency graph in make syntax, let's first go over it graphically. figure 12.3 shows a graphical representation of testintmath dependency graph.
* each node represents a file, and a directed edges represent dependencies.&#x20;

<figure><img src="../.gitbook/assets/Group 125 (1).png" alt="" width="563"><figcaption><p>Figure 12.3: testintmath's dependency graph</p></figcaption></figure>



In make syntax, dependency graphs are represented by dependency rules. We create what is known as a _dependency rule_ for each target in the dependency graph--`testintmath.o`, `intmath.o`, and `testintmath`. Dependency rules have the following syntax:

```
target: dependencies
<tab> command
```

* **Dependencies**. The files that the target _directly_ depends on (e.g., `testintmath` directly depends on `testintmath.o` and `intmath.o`).
* **Command**. The command to build the target (e.g., the command to build `testintmath` is `gcc217 intmath.o testintmath.o -o testintmath`). Note that the command _must_ be preceded by a Tab character. Failure to do so will result in an error.

This results in the following makefile:

```makefile
testintmath: testintmath.o intmath.o
    gcc217 testintmath.o intmath.o -o testintmath

testintmath.o: testintmath.c intmath.h
    gcc217 -c testintmath.c

intmath.o: intmath.c intmath.h
    gcc217 -c intmath.c
```
