# Motivation for Make

Imagine you're working on a multi-file C project and you make a few minor changes to your codebase. The next step is to rebuild your executable to see those changes take effect. If your project is on the smaller side, recompiling all source files is a reasonable approach. But, what if your project is on the larger side, say consisting of 1000 source files? In such a scenario, recompiling every single source file would be extremely time-consuming and a drain on system resources. Thankfully, there's no need to go down that road. You can adopt a more efficient approach, recompiling only the files that were changed or affected by the changes.

In this chapter, we will discuss two ways of doing so. First, we will discuss the manual approach. Then we will discuss how to do it with make.&#x20;

#### Partial builds: Manual Approach

As an example, we will use the program shown in Figure 1, which consists of three source files: intmath.c, testintmath.c, and intmath.h.&#x20;

The key to partial builds involves building our program in two main steps. In the first step, we invoke gcc on intmath.c and testintmath.c with the -c option:&#x20;

```
gcc -c intmath.c testintmath.c
```

This instructs gcc to translate intmath.c and testintmath.c independently into object files--intmath.o and testintmath.o respectively--which are machine code representations of their source files. Note that we do not specify the header file intmath.h on the command line, since its contents are included in intmath.c and testintmath.c via their #include directives. &#x20;

In the second step, we invoke gcc intmath.o and testintmath.o:

```
gcc intmath.o testintmath.o -o testintmath
```

which links the two object files together to produce the executable testintmath. This process is summarized in Figure 1.&#x20;











<figure><img src="../.gitbook/assets/Screenshot 2024-02-05 at 6.58.16 PM.png" alt=""><figcaption></figcaption></figure>
