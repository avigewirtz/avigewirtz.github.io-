# Background

In this chapter, we will discuss the make tool. We'll start out by explaining the motivation for make, using the program testintmath as an example. We'll then explain how to build testintmath with make.&#x20;

## Motivation for Make

Imagine you’re working on a C program consisting of 1000 source files and you make a change to just one file. You wouldn't want to recompile all 1000 files for this single change to take effect, as it would be extremely time-consuming. Instead, you’d want to recompile only the file you've updated. Thankfully, GCC (and other C compilers) enable you to do just that.&#x20;

\


In our discussion about GCC, recall that GCC transforms source files into an executable in two main stages:

\


1. Translation phase: In the first phase, GCC translates each C file (.c) independently into an object file (.o).
2. Linking phase: GCC then links the object files together to form an executable file.&#x20;

\


This two-stage compilation design isn’t arbitrary. In fact, it’s precisely what enables partial builds.&#x20;

\


EXPLAIN HOW SEPARATE COMPILATION ENABLED US TO AVOID REDUNDANT COMPILATION

\


We think of compilation as a two step process. The first step involves translation to object files. The second step involves generating an executable by linking the object files.&#x20;

\


* Convert each source file to an object file
* Link the object files to produce an executable file

When building your program, you think of it as follows:&#x20;

\


* Were any source files changed? If so, compile those files only.&#x20;
* All object files must always be re-linked.&#x20;

\


If there are updated in the source files, that will lead to one or more of the object files being out of date. We call those source files a dependency. The first step to determining what needs to be recompiled is determining which files it depends on. The second step is determining what command needs to be executed to get the object file up to date.&#x20;

\


To capitalize on this, the strategy involves two main steps:

1. Save object files: Whenever you invoke GCC on .c file, ensure to save the resulting object file. The object file represents the machine code version of that specific source file.
2. Selectively compile: Don’t invoke GCC on a .c file if it will result in an object file identical to the one you already have.&#x20;

A practical method to determine when object files need to be rebuilt is to use a dependency graph.&#x20;

\


Let's illustrate this strategy by means of a simple program composed of three files: intmath.c, testintmath.c, and intmath.h. Their source code is shown in Figure 1. Let’s follow the strategy outlined above. First, we build our program, but we ensure to save all intermediate object files. How do we save object files?&#x20;

\


We could invoke gcc with the –save-temps option, which instructs gcc to save all intermediate files. However, this approach is not ideal, since gcc will also save the preprocessed (.i) and compiled (.s) versions, which we don’t need. Unfortunately, gcc doesn’t offer any option to build a program and save only the object files in a single command. Instead, we build our program using two commands. The first command is gcc with the -c option:

\


gcc -c intmath.c testintmath.c&#x20;

\


This command translates intmath.c and testintmath.c into object files intmath.o and testintmath.o, respectively. We then link the object files together to form an executable file (which we’ll name testintmath) using the following command:

\


gcc intmath.o testintmath.o -o testintmath

\


This entire process is shown in Figure 3. Note the linking phase also includes object files from the C standard library.&#x20;

\
\
\
\
\
\


If you check your directory, you’ll notice you now have 6 files: intmath.c, testintmath.c, intmath.h, intmath.o, testintmath.o, and testintmath.&#x20;

\


Intmath.c, testintmath.c, and testintmath are the source files, while intmath.o, testintmath.o, and testintmath are the target files. To determine what sort of recompilation will be necessitated by changing one or more of the source files, let’s draw a dependency graph.&#x20;

\


If we modify intmath.c, then we will have to recompile it.

\
\
\
\


Now, let's consider a scenario where we want to update the LCM and GCD functions in intmath.c by inserting assert statements, as shown in Figure 2.

\


\#include "intmath.h"

\#include \<assert.h>

\


int gcd(int i, int j)

{

&#x20;  int temp;

\


&#x20;  assert(i > 0);

&#x20;  assert(j > 0);

\


&#x20;  while (j != 0)

&#x20;  {

&#x20;    temp = i % j;

&#x20;    i = j;

&#x20;   j = temp;

&#x20;  }

\


&#x20;  return i;

}

\
\


int lcm(int i int j)

{

&#x20;  assert(i > 0);

&#x20;  assert(j > 0);

\


&#x20;  return (i / gcd(i, j)) \* j;

\
\
\


To generate an updated executable, we need not recompile testintmath.c, since it was not affected by the changes in intmath.c. Instead, we invoke gcc with the -c option on testintmath.c alone:&#x20;

\


gcc -c  intmath.c

\


Then we link the resulting updated intmath.o with the “old” testintmath.o to produce an updated executable:&#x20;

\


gcc intmath.o testintmath.o -o testintmath&#x20;

\


If we were not to update testintmath.c, the process would be the same. We would recompile only testintmath.c, and then link the updated testintmath.o. If we update intmath.h, however, both intmath.c and testintmath.c would have to be recompiled. This is because \<fil in>.

\
\


<figure><img src="../.gitbook/assets/Group 104.png" alt="" width="563"><figcaption></figcaption></figure>





```c
/*--------------------------------------------------------------------*/
/* intmath.c                                                      */
/*--------------------------------------------------------------------*/

#include "intmath.h"

int gcd(int i, int j)
{
int temp;
while (j != 0) {
temp = i % j;
i = j;
j = temp;
}
return i;
}
int lcm(int i, int j)
{
return (i / gcd(i, j)) * j;
}
```

```c
/*--------------------------------------------------------------------*/
/* testintmath.c                                                      */
/*--------------------------------------------------------------------*/

#include <stdio.h>
#include "intmath.h"

int main(void)
{
int i, j;
printf("Enter the first integer:\n"); scanf("%d", &i);
printf("Enter the second integer:\n"); scanf("%d", &j);
printf("Greatest common divisor: %d.\n", gcd(i, j));
printf("Least common multiple: %d.\n", lcm(i, j));
return 0; 
}
```

```c
/*--------------------------------------------------------------------*/
/* intmath.h */
/*--------------------------------------------------------------------*/
#ifndef INTMATH_INCLUDED 
#define INTMATH_INCLUDED 
int gcd(int i, int j); 
int lcm(int i, int j); 
#endif
```

