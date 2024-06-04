# Introduction

In a nutshell, `make` is a software tool that automates the process of incremental builds. The premise behind incremental builds is simple: after you change source files and want to rebuild your program, you rebuild only the affected files, instead of wasting time and rebuilding the entire program. This is especially important in large projects, where build times can become a bottleneck. As we'll see soon, however, implementing incremental builds manually is tedious and error-prone. For that reason, the `make` tool was developed, which automates the process.

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

#### Building testintmath: The Non-incremental Build Approach

The non-incremental build approach, which we've using thus far, is as simple as it gets. Each time we want to build `testintmath`, we run the following command: 

```bash
gcc217 testintmath.c intmath.c -o testintmath
```

We use this command whether we're building our program for the first time, the tenth time, or the one hundredth time. In other words, we don't take into consideration which files were modified since the last build. We just rebuild the whole program. &#x20;

#### Building testintmath: The Incremental Build Approach

Recall what happens under the hood when we build `testintmath`. First, `gcc` preprocesses, compiles, and assembles `testintmath.c`, producing relocatable object files `testintmath.o`. Next, `gcc` preprocesses, compiles, and assembles `intmath.c`, producing relocatable object file `intmath.o`. In the preprocessing stage, `intmath.h` is inserted into each file. Finally, `gcc` links `testintmath.o` and `intmath.o`--along with necessary relocatable object files form C library--to produce executable object file `testintmath`. Recall that by default, `gcc` discards the relocatable object files. The approach we showed before was essentially a shortcut to perform all steps via a single command. This processed is shown in Figure 8.&#x20;

<figure><img src="../.gitbook/assets/Group 234 (3).png" alt="" width="375"><figcaption></figcaption></figure>

Notice that `testintmath.o` is derived from `testintmath.c` and `intmath.o` only, that is, it is not in any way derived form `intmath.c`. Similarly, `intmath.o` is derived from `intmath.o` and intmath.h only. It follows that changes to `testintmath.c` do not affect `intmath.o`, and changes to `intmath.c` do not affect `testintmath.o`.&#x20;

In the previous example, we rebuilt both `intmath.o` and `testintmath.o` even if only a single `.c` file such as `intmath.c` was modified. That was wasteful, however, since `testintmath.o` was not affected by a modification to `intmath.c`. We could have rebuilt only `intmath.o` and then linked it with `testintmath.o` generated from the previous build. Had we have retained `testintmath.o`, that is.&#x20;

gcc does not offer any shortcut option to build a program in a single command and retain the relocatable object files. Recall, however, that you can save object files using the `-c` option . This instructs gcc to stop after assembly and output the `.o` files. You can then link the .o files by invoking as usual. Thus, to build our program and save the object files, we build our program with the following two command:

```
gcc217 -c testintmath.c intmath.c
gcc217 testintmath.o intmath.o -o testintmath
```

Now, with the object files in hand, the next time we build our program, we rebuild only the affected object files(s) and then link them to produce an uipdated executable. For example, if we modify intmath.c, we rebuild intmath.o only, and then link intmath.o with testintmath.o, producing the updated executable testintmath:

```
gcc217 -c intmath.c
gcc217 testintmath.o intmath.o -o testintmath
```

This incremental build appraoch is shown in Figure 13.

<figure><img src="../.gitbook/assets/Group 239 (1).png" alt=""><figcaption></figcaption></figure>

Notice that if we modify `intmath.h`, we'd have to rebuild the entire program. In general, changes to header files are much more dramatic than changes to `.c` files. Changes to .c files typically only affect one .o file, where changes to header files often affect many `.o` files.&#x20;

{% hint style="info" %}
It's important to understand that, fundamentally, the underlying GCC build process is the same irrespective of whether we build our program via two commands:

```bash
gcc217 -c intmath.c testintmath.c
gcc217 intmath.o testintmath.o -o testintmath
```

Or via single command:

```bash
gcc217 intmath.c testintmath.c -o testintmath
```

The only difference between these two approaches is that the two-command approach retains the`.o` files while the single-command approach does not.
{% endhint %}

#### Challenges of manually implementing Incremental Builds

As this example shows, implementing incremental builds manually is possible but it requires you to:

1. Keep track of which source files have been modified since the last build.
2. Understand which object files are affected by these changes.
3. Rebuild in the correct sequence, that is, .o files before executable. Trivial in our case, but in real life

Even for a small program like testintmath, this task isn’t particulurly exciting, though it is reasonably manageable. As programs grow larger, however, and the web of dependencies grows increasingly complex, this task becomes incredibly tedious and error-prone.

Consider a scenario, for example, where you modify a header file `A`, that is `#included` in, say, 20 of your program's `.c` files. You’d have to track down each one of these `.c` files and recompile it. Worse yet, imagine header file `A` is also `#include`d in header file `B`. You'd then have to also track down all `.c` files that `#include` `B` and recompile them.

For this reason, the `make` tool was developed, which automates the process of incremental builds. The section that follows describes how to use make.
