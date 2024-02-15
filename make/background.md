# Motivation for Make

Imagine working on a C program consisting of 1000 source files, and you make a change to just one .c file. To incorporate the change, you need to rebuild the executable. Having to recompile all 1000 source files due to a change in just one would be extremely time-consuming and a drain on system resources.  Thankfully, there's no need to go down that route. Long ago, a rather elegant solution was developed, called _separate compilation_. In this scheme, rather than compiling a multi-file program as a monolithic unit, each source file is compiled independently into an object file and then linked together to form the final executable. This process is shown in Figure 1. The benefit of this approach is that you can retain the object files for future use, thus not having to rebuild object files that would be unaffected by changes.&#x20;

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

Becuase both files have .o extensions, GCC deduces that no compilation is needed, and thus begins with the linking stage. Note that GCC will also link necessary files from the C standard library, such as the the files which contain the printf() and scanf() functions.&#x20;



### Testintmath Dependencies





To be a little more formal, a file B is said to depend on a file A if a change in B requires A to be updated.





























We know from the chapter on GCC that a multi-file C program&#x20;





Imagine you’re working on a multi-file C program and make changes to just one .c file. To incorporate the changes, the next step is to rebuild the executable.&#x20;

The simplest approach to&#x20;

The beginner approach is as straightforward as it gets. Every time you make a change, no matter how small, you recompile every file in the project. It’s super easy to do because you don’t have to think about what’s changed or how different parts of your project depend on each other. The downside? It can be a huge waste of time, especially for larger projects, since you’re recompiling stuff that hasn’t changed at all.&#x20;

The manual approach involves a more selective approach, where you only recompile the files that were affected by the changes you made. This method asks for a bit more brainpower because you need to figure out exactly which files need recompiling. It’s much more efficient since you’re not wasting time recompiling unchanged files, but it can be tricky to get right, especially in complex projects with lots of interdependencies.&#x20;

The automated approach involves automating approach 2 via a build tool like make. This is where technology comes in handy, offering both efficiency and ease of use. make automates the process of figuring out which files need to be recompiled when changes occur. You set up a Makefile that describes the dependencies between your files, and the tool takes it from there, only recompiling what’s necessary based on your changes.

\<explain that the aim of this chapter is explain how to use make. in order to do so, we'll first go over the manual approach. explain why>



<figure><img src="../.gitbook/assets/Screenshot 2024-02-05 at 6.58.16 PM.png" alt=""><figcaption></figcaption></figure>

## Approach 1:&#x20;

The simplest appraoch to dealing with chanages in the source code is recompiling the entire codebase. With testintmath, we'd use the following command, whether where  building it for the first time or updatating it after a change to one of it's source files, such as intmath.c:&#x20;

```
gcc intmath.c testintmath.c -o testintmath
```

The upside to this approach \<fill in>

The downside \<fill in>&#x20;

This approach is as straightforward as it gets, since you don’t have to think about what’s changed or how different parts of the program depend on each other. You just compile the whole thing. The downside, however, is that It can be a huge waste of time, especially for larger projects, since you’re recompiling stuff that hasn’t changed at all.

## Approach 2:

The second approach to building testintmath is more selective, where we only compile the files that were changed or affected by changes.&#x20;
