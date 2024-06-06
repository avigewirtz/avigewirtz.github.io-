# Introduction

In a nutshell, `make` is a software tool that automates the process of incremental builds. The premise behind incremental builds is simple: when you rebuild your program after making a change to the source code, you rebuild only the affected files, not the entire program. This is especially important in large projects, where build times can become a bottleneck.

In this chapter, we'll first describe how to implement incremental builds manually. Then, we'll discuss how to automate the process with make.

#### Review: GCC Build Process

Before we can discuss incremental builds, we need to refresh our memory on the GCC build process. In particular, recall the following:&#x20;

* GCC preprocesses, compiles, and assembles each file independntly. to produce the executable, gcc links all .o files
* in preprocessing stage headers included
* If we invoke gcc without any options to control the build process, gcc will perform all stages and output only the executable. In other words, none of the intermediate object files will be retained.
* To retain the .o files, we can build our program in two steps. First, we we can first invoke gcc with -c option, which instructs to halt after assembly and output the .o files. Next&#x20;

#### How incremental builds work

As you may have guessed, the key to incremental builds is saving .o files and reusing them in later builds. Notice in figure 12 that each .o file is derived from its correspinding .c file, as well as any files included in the .c file. It is not derived from any other source file. It follows that so long as you retian object files from the previous build, you need to only rebuild the affected object files. You then link the updated object files with the new object files to produce an updated executable.&#x20;

More formally, we can capture the dependencies of a program via a dependency graph. In this graph, nodes represent files, and directed edges represent dependencies. If A -> B, then A directly depends on B, meaning that a change to B requires A to be rebuilt. If A -> B and B -> C, then A indirectly (or transitively) depends on C, meaning a change to C requires B to be rebuilt, which in turn requires A to be rebuilt. A dependency graph for our foobarbaz program is shown in Figure 13.&#x20;









#### Incremental Builds in Action

As a running example throughout this chapter, we'll use the `testintmath` program from precept 4, comprised of three files: `testintmath.c`, `intmath.c`, and `intmath.h`. For reference, the source code is provided below.

{% tabs %}
{% tab title="testintmath.c (client)" %}
{% code lineNumbers="true" %}
```c
/*--------------------------------------------------------------------*/
/* testintmath.c                                                      */
/* Author: Bob Dondero                                                */
/*--------------------------------------------------------------------*/

#include "intmath.h"
#include <stdio.h>
#include <stdlib.h>

/* Read two positive integers from stdin. Return EXIT_FAILURE if stdin
   contains bad data. Otherwise compute the greatest common divisor
   and least common multiple of the two positive integers, write those
   two values to stdout, and return 0. */

int main(void)
{
   int i1;
   int i2;
   int iGcd;
   int iLcm;
   int iScanfReturn;

   printf("Enter the first positive integer:\n");
   iScanfReturn = scanf("%d", &i1);
   if ((iScanfReturn != 1) || (i1 <= 0))
   {
      fprintf(stderr, "Error: Not a positive integer.\n");
      exit(EXIT_FAILURE);
   }

   printf("Enter the second positive integer:\n");
   iScanfReturn = scanf("%d", &i2);
   if ((iScanfReturn != 1) || (i2 <= 0))
   {
      fprintf(stderr, "Error: Not a positive integer.\n");
      exit(EXIT_FAILURE);
   }

   iGcd = IntMath_gcd(i1, i2);
   iLcm = IntMath_lcm(i1, i2);

   printf("The greatest common divisor of %d and %d is %d.\n",
      i1, i2, iGcd);
   printf("The least common multiple of %d and %d is %d.\n",
      i1, i2, iLcm);

   return 0;
}
```
{% endcode %}
{% endtab %}

{% tab title="intmath.c (implementation)" %}
```c
/*--------------------------------------------------------------------*/
/* intmath.c                                                          */
/* Author: Bob Dondero                                                */
/*--------------------------------------------------------------------*/

#include "intmath.h"
#include <assert.h>

int IntMath_gcd(int iFirst, int iSecond)
{
   int iTemp;

   assert(iFirst > 0);
   assert(iSecond > 0);

   /* Use Euclid's algorithm. */

   while (iSecond != 0)
   {
     iTemp = iFirst % iSecond;
     iFirst = iSecond;
     iSecond = iTemp;
   }

   return iFirst;
}

int IntMath_lcm(int iFirst, int iSecond)
{
   assert(iFirst > 0);
   assert(iSecond > 0);

   return (iFirst / IntMath_gcd(iFirst, iSecond)) * iSecond;
}
```
{% endtab %}

{% tab title="intmath.h (interface)" %}
```c
/*--------------------------------------------------------------------*/
/* intmath.h                                                          */
/* Author: Bob Dondero                                                */
/*--------------------------------------------------------------------*/

#ifndef INTMATH_INCLUDED
#define INTMATH_INCLUDED

/* Return the greatest common divisor of positive integers iFirst and
   iSecond. */

int IntMath_gcd(int iFirst, int iSecond);

/* Return the least common multiple of positive integers iFirst and
   iSecond. */

int IntMath_lcm(int iFirst, int iSecond);

#endif
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
It's important to understand that, fundamentally, the underlying GCC build process is the same irrespective of whether we build our program via two commands:

```bash
gcc217 -c intmath.c testintmath.c
gcc217 intmath.o testintmath.o -o testintmath
```

Or via a single command:

```bash
gcc217 intmath.c testintmath.c -o testintmath
```

The only difference between these two approaches is that the two-command approach retains the`.o` files while the single-command approach does not.
{% endhint %}

#### Challenges of Manually Implementing Incremental Builds

As this example shows, implementing incremental builds manually is possible but it requires some work. In particular, you have to:

1. Keep track of which `.c` and `.h` files were modified since the last build.
2. Know which `.o` files depend on the modified `.c` and `.o` files.

Even for a small program like `testintmath`, this task isn’t particularly fun, though it is admittedly manageable. As programs grow larger, however, and the web of dependencies grows increasingly complex, this task becomes incredibly tedious and error-prone.

Consider a scenario where you modify header file `A`, which is `#included` in, say, 20 `.c` files. You’d have to track down and recompile all these `.c` file. Worse yet, imagine header file `A` is also `#included` in header file `B`. You'd then have to also track down and recompile all the `.c` files that `#include` `B`.

To make life easier (no pun intended), the `make` tool was developed, which automates the process of incremental builds. In the next section, we describe how to use `make`.
