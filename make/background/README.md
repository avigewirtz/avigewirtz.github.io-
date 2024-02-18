# Motivation for Make

## Introduction

Imagine working on a C program consisting of 1000 source files, and you make a change to just one .c file. To incorporate the change, you'd need to rebuild the executable. Having to recompile all 1000 source files due to a change in just one would be extremely time-consuming and a drain on system resources.  Thankfully, there's no need to go down that route. Long ago, an elegant solution called _separate compilation_ was developed. In this scheme, rather than compiling a multi-file program as a monolithic unit, each source file is compiled independently into an object file and then linked together to form the final executable. This process is shown in Figure 1. The benefit of this approach is that you can retain the object files for future use, thus not having to rebuild object files that would be unaffected by changes.&#x20;

At first glance, implementing this strategy might seem straightforward. Before rebuilding an executable, you compare the timestamps of all source files with the timestamps of the executable, and if a source file is newer than the executable, you recompile just those source files. Unfortunately, the process is far more complex. In addition to keeping track of which files changed, you also have to keep track of dependencies.&#x20;

It is precisely these frustrations that led Stuart Feldman to create the make program in 1978. In a nutshell, make is a program that automates this process...&#x20;

Once you set up an appropriate makefile, you build your program by simple invoking:

```
make
```

and make figures out for you the minimum required number of files that have to be recompiled, and invokes the necessary commands.&#x20;

In this chapter, we will go over the basics of how make works and setting up a makefile. To set the stage, we will first go over the manual approach. As a running example, we'll use the testintmath program from precept 4, shown in Figure 1.&#x20;



## Separate compilation: Manual Approach

Suppose we just created the three source files and are building testintmath for the firs time.&#x20;

Rather than using the familiar command `gcc intmath.c testintmath.c -o testintmath`, which does not retain the resulting object files, we build our program in two steps. First, we invoke gcc on each .c file with the -c option, which tells GCC to generate object files, but not link them. We can invoke GCC on each .c file individually:

```
gcc -c intmath.c
gcc -c testintmath.c
```

Or we can invoke gcc on both files together:

```
gcc -c intmath.c testintmath.c
```

The result is the same. If you invoke ls, you'll see that you now have object files:

```
-> ls
intmath.c intmath.o testintmath.c testintmath.o
```

We need include intmath.h even though it is part of the source code for our program, since it is included by the preprocessor.&#x20;

The second step is to invoke GCC to link intmath.o and testintmath.o together. To specify that we want the executable to be named testintmath (rather than the default a.out), we use the -o option:&#x20;

```
gcc intmath.o testintmath.o -o testintmath
```

Becuase both files have .o extensions, GCC deduces that no compilation is needed, and thus begins goes immediately to linking. Note that GCC will also link necessary files from the C standard library, such as the the files which contain the printf() and scanf() functions.&#x20;

<figure><img src="../../.gitbook/assets/Group 28 (1).png" alt=""><figcaption></figcaption></figure>

### Rebuilding testintmath

If we are to make changes to our program, our objective is to generate a new executable by recompiling the minimum necessary files. To do this accurately, we need to have a thorough understanding of the program's dependencies, which can be visualized using a dependency graph.

In such a graph, each node represents a file, and directed edges (arrows) between these nodes indicate a dependency, where an edge from file A to file B signifies that B is dependent on A. In other words, a change in file A requires file B to be updated. A dependency graph for testintmath is shown in Figure 2.&#x20;

&#x20;

<figure><img src="../../.gitbook/assets/Group 41.png" alt=""><figcaption></figcaption></figure>



<figure><img src="../../.gitbook/assets/Group 39.png" alt=""><figcaption></figcaption></figure>

## Separate compilation: Make approach





























<figure><img src="../../.gitbook/assets/Screenshot 2024-02-05 at 6.58.16 PM.png" alt=""><figcaption></figcaption></figure>

