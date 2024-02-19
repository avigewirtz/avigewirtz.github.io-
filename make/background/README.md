# Motivation for Make

## Introduction

Imagine you're working on a C program consisting of 1000 source files, and you make a change to just one .c file. To incorporate the change, you'd need to rebuild the executable. Having to recompile all 1000 source files due to a change in just one would be extremely time-consuming and a drain on system resources.  Thankfully, there's no need to go down that route. Long ago, an elegant solution called _separate compilation_ was developed. In this scheme, rather than compiling a multi-file program as a monolithic unit, each source file is compiled independently into an object file and then linked together to form the final executable. This process is shown in Figure 1. The benefit of this approach is that you can retain the object files for future use, thus not having to rebuild object files that would be unaffected by changes.&#x20;

At first glance, implementing this strategy might seem straightforward. Before rebuilding an executable, you compare the timestamps of all source files with the timestamps of the executable, and if a source file is newer than the executable, you recompile just those source files. Unfortunately, the process is far more complex. In addition to keeping track of which files changed, you also have to keep track of dependencies.&#x20;

It is precisely these frustrations that led Stuart Feldman to create the make program in 1978. In a nutshell, make is a program that automates this process...&#x20;

Once you set up an appropriate makefile, you build your program by simple invoking:

```
make
```

and make figures out for you the minimum required number of files that have to be recompiled, and invokes the necessary commands.&#x20;

In this chapter, we will go over the basics of how make works and setting up a makefile. To set the stage, we will first go over the manual approach. Then we'll go over how to do it using make.&#x20;



## Separate compilation: Manual Approach

As a running example throughout this chapter, we'll use the testintmath program from precept 4, shown in Figure 1.&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2024-02-05 at 6.58.16 PM.png" alt=""><figcaption><p>Figure 1: testintmath program</p></figcaption></figure>

To build testintmath, rather than using the familiar command, `gcc intmath.c testintmath.c -o testintmath`--which would generate the executable testintmath but would not retain the intermediate object files--we'll use appraoch shown in Figure 2. In this approach, we we first invoke gcc on each .c file with the -c option, which compiles intmath.c and testintmath.c into object files--intmath.o and testintmath.o respectively--but does not link them. Then we invoke gcc on the object files intmath.o and testintmath.o, which links them--along with necessary library code--tigether to form the executable testintmath.  Note that we do not include header files on command line, since they're included via #include directives.&#x20;

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
