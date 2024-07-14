# Introduction

In a nutshell, `make` is a software tool that automates the process of incremental builds. The premise behind incremental builds is simple: When you rebuild your program after making a change to the source code, you rebuild only the affected files, not the entire program. This is especially important in large projects, where build times can become a bottleneck.

In this chapter, we'll first describe how incremental builds work in C. Then, we'll show how to automate the process with `make`. As a running example throughout this chapter, we'll use the `testintmath` program from [Building Multi-file Programs](../gcc-build-process/page-1-1.md). For reference, its source code is provided below.&#x20;

{% tabs %}
{% tab title="testintmath.c" %}
{% code lineNumbers="true" %}
```c
/*--------------------------------------------------------------------*/
/* testintmath.c                                                      */
/*--------------------------------------------------------------------*/

#include "intmath.h"
#include <stdio.h>
#include <stdlib.h>

/*--------------------------------------------------------------------*/

/* Read two positive integers from stdin. Return EXIT_FAILURE if stdin
   contains bad data and an write error message to stderr. Otherwise
   compute the greatest common divisor and least common multiple of
   the two positive integers, write those two values to stdout, and
   return 0. */

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

   iGcd = gcd(i1, i2);
   iLcm = lcm(i1, i2);

   printf("The greatest common divisor of %d and %d is %d.\n",
      i1, i2, iGcd);
   printf("The least common multiple of %d and %d is %d.\n",
      i1, i2, iLcm);

   return 0;
}
```
{% endcode %}
{% endtab %}

{% tab title="intmath.c " %}
{% code lineNumbers="true" %}
```c
/*--------------------------------------------------------------------*/
/* intmath.c                                                          */
/*--------------------------------------------------------------------*/

#include "intmath.h"

/*--------------------------------------------------------------------*/

int gcd(int iFirst, int iSecond)
{
   int iTemp;

   /* Use Euclid's algorithm. */

   while (iSecond != 0)
   {
      iTemp = iFirst % iSecond;
      iFirst = iSecond;
      iSecond = iTemp;
   }

   return iFirst;
}

/*--------------------------------------------------------------------*/

int lcm(int iFirst, int iSecond)
{
   return (iFirst / gcd(iFirst, iSecond)) * iSecond;
}
```
{% endcode %}
{% endtab %}

{% tab title="intmath.h " %}
```c
/*--------------------------------------------------------------------*/
/* intmath.h                                                          */
/*--------------------------------------------------------------------*/

/* Return the greatest common divisor of positive integers iFirst and
   iSecond. */

int gcd(int iFirst, int iSecond);

/*--------------------------------------------------------------------*/

/* Return the least common multiple of positive integers iFirst and
   iSecond. */

int lcm(int iFirst, int iSecond);
```
{% endtab %}
{% endtabs %}
