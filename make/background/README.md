# Introduction

At its core, "make" is a build automation tool that simplifies the process of building multi-file programs. It uses a file known as a Makefile, which contains a set of directives for compiling the software. These directives include rules, dependencies, and actions that define how to compile and link the program.

##

##

## Building multi-file programs

As a running example throughout this chapter, we'll use the testintmath program from precept 4, shown in Figure 1.&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2024-02-05 at 6.58.16 PM.png" alt=""><figcaption><p>Figure 1: testintmath program</p></figcaption></figure>



<figure><img src="../../.gitbook/assets/Group 55.png" alt=""><figcaption></figcaption></figure>

## Building testintmath: Brute-force appraoch





















The strategy is simple. First, we build our program as usual, but we ensure testintmath, we ensure to save the intermediate object files. To build testintmath, we'll use a two-step approach. First, we invoke gcc with the -c flag on each .c file:

```
gcc -c intmath.c 
gcc -c testintmath.c
```

This preprocesses, compiles, and assembles intmath.c and testintmath.c, generating the object files intmath.o and testintmath.o. Note that in the preprocessing stage of both intmath.c and testintmath.c, the contents of intmath.h are included into them. &#x20;

rather than using the familiar command, `gcc intmath.c testintmath.c -o testintmath`--which would generate the testintmath executable but would not retain the intermediate object files--we'll use the approach shown in Figure 2. In this approach, we first invoke gcc on each .c file with the -c option:

```bash
gcc -c intmath.c testintmath.c
```

This preprocesses, compiles, and assembles intmath.c and testintmath.c, producing the object files intmath.o and testintmath.o. Note that in the preprocessing stage of both intmath.c and testintmath.c, the contents are intmath.h were inserted into each.  Thus, `intmath.o` is derived from both `intmath.c` and `intmath.h`. Similarly, testintmath.o is derived from both `intmath.c` and `intmath.h`.



We then link intmath.o and testintmath.o, generating the testintmath executable:&#x20;

```
gcc intmath.c testintmath.c -o testintmath
```



<figure><img src="../../.gitbook/assets/Group 28 (1).png" alt=""><figcaption></figcaption></figure>



### Rebuilding testintmath

Now imagine we make a change to one of our source files. Our goal is to rebuild testintmath by recompiling the minimum necessary source files. An easy way to figure our what changes require which files to be rebuilt is via a dependency graph.&#x20;











&#x20; recompile the mininum  To rebuild testintmath, we need only recompile intmath.c

\<over here i want to explain how if we make changes we can use partial builds to rebuild testintmath. i want to explain using a dependency graph of testintmath, where each node represents a file, and directed edges (arrows) between these nodes indicate a dependency, where an edge from file A to file B signifies that B is dependent on A. In other words, a change in file A requires file B to be updated.>









<figure><img src="../../.gitbook/assets/Group 28 (1).png" alt=""><figcaption></figcaption></figure>





our objective is to generate a new executable by recompiling the minimum necessary files. To do this accurately, we need to have a thorough understanding of the program's dependencies, which can be visualized using a dependency graph.

In such a graph, each node represents a file, and directed edges (arrows) between these nodes indicate a dependency, where an edge from file A to file B signifies that B is dependent on A. In other words, a change in file A requires file B to be updated. A dependency graph for testintmath is shown in Figure 2.&#x20;

&#x20;

<figure><img src="../../.gitbook/assets/Group 41.png" alt=""><figcaption></figcaption></figure>



<figure><img src="../../.gitbook/assets/Group 39.png" alt=""><figcaption></figcaption></figure>
