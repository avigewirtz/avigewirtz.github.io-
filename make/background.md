# Introduction

In a nutshell, `make` is a software tool that automates the process of incremental builds.The premise behind incremental builds is simple: after you change source files and want to rebuild your program, you rebuild only the affected files, instead of wasting time and rebuilding the entire program. This is especially important in large projects, where build times become a bottleneck. The key to understanding `make` is understanding how incremental builds work and how to implement them manually. Once you understand this, the mechanics and role of `make` become apparent.

#### Running Example

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

#### Building testintmath: the non-incremental build approach



The current approach we've been using is to build out program with the following command:

gcc ...

suppose we change add.c. we rebuild our program by invoking the same command again:

Incremental builds

Recall what happens under the hood when we built our program. each file, along with all files included, is independently preprocessoed, compiled, and assembled, producing .o files. then, the .o files are linked, producing the executable.

in the previous example, we recompiled all source files after only add.c was modified. we were affectivelt treating the entire program as a monolithic unit, wheere all files are always compiled at the same time. notice, however, that the only files affected by the change were add.o and calc. calc.o and mult were not affected. thus, had we have saved the object files from the last build, we could have rebuilt the program by rebuilding add.o alone and then linking it with the "old" object files.

recall that you can save object files with the -c option. it instructs gcc to halt after assembly and output the .o files. thus, the incremental build approach would have been to invoke gcc on all files with the -c

* the key is saving object files and tracking dependencies

{% hint style="success" %}
Fundamentally, the underlying GCC build process is the same irrespective of whether we build our program via two commands:

```bash
gcc217 -c intmath.c testintmath.c
gcc217 intmath.o testintmath.o -o testintmath
```

Or via single command:

```bash
gcc217 intmath.c testintmath.c -o testintmath
```

The only difference between the two-command and single-command approaches is that the former retains the intermediate object files while the latter does not.
{% endhint %}

#### Challenges of manually implementing Incremental Builds

As this example shows, implementing incremental builds manually is possible but it requires you to:

1. Keeo track of which source files have been modified since the last build.
2. Understand which object files are affected by these changes.

Even for a small program like testintmath, this task isn’t particulurly exciting, though it is reasonably manageable. As programs grow larger, however, and the web of dependencies grows increasingly complex, this task becomes incredibly tedious and error-prone.

Consider a scenario, for example, where you modify a header file `A`, that is `#included` in, say, 20 of your program's `.c` files. You’d have to track down each one of these `.c` files and recompile it. Worse yet, imagine header file `A` is also `#include`d in header file `B`. You'd then have to also track down all `.c` files that `#include` `B` and recompile them.

For this reason, the `make` tool was developed, which automates the process of incremental builds. The section that follows describes how to use make.
