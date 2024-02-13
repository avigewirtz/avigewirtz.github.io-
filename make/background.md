# Motivation for Make

Imagine you working on a C project and you make changes to a few files. The next step is to rebuild your executable to see those changes take effect. If your project is on the smaller side, you can rebuild your project by simply recompiling every source file. Although it may seem like overkill to But, what if your project is on the larger side, say consisting of 1000 source files? In such a scenario, recompiling every single source file would be extremely time-consuming and a drain on system resources. Thankfully, there's no need to go down that road. You can adopt a more efficient approach, recompiling only the files that were changed or affected by the changes.

In this chapter, we will focus on the most efficient approach of doing so--using a build system like make. To motivate your understanding of how make works and your appreictation for the benefits it offers, we will first go over how to do this maually, using basic gcc commmands.&#x20;

#### Partial builds: Manual Approach

As an example, we will use the program shown in Figure 1, which consists of three source files: intmath.c, testintmath.c, and intmath.h.&#x20;

If you're familiar with the GCC compilation process, which we discusssed in chapter 4 on GCC, what follows here will flow smoothly. If you are not, then it wont make much sense. In that case, it is advised that you first study chapter 4.&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2024-02-05 at 6.58.16 PM.png" alt=""><figcaption></figcaption></figure>

The key to partial builds is building a program in two steps

In the first step, we invoke GCC with the -c option on all .c files that need to be compiled. The first time we build testintmath, that's intmath.c and testintmath.c:

```
gcc -c intmath.c testintmath.c
```

This command translates intmath.c and testintmath.c into the object files intmath.o and testintmath.c respectively. Note that we do not specify the header file intmath.h on the command line, since its contents are included in intmath.c and testintmath.c via the #include directive in both files. &#x20;

In the second step,&#x20;

. In the first step, each .c file is translated separately into an object file. In this approach, the source files are translated separately and then linked together—a two stage process.

The key to partial builds is separate compilation. In this approach, each .c file is translated independently into an object file.&#x20;





The strategy is to build our program in two steps. In the first step, we invoke gcc with the -c option:&#x20;





The strategy for selective compilation is as follows.&#x20;

Whenever we invoke gcc on a .c file, we We will build this program in two steps. In the first step, we'll invoke gcc with the -c option,&#x20;

* then go over dependency's / dependency graph
