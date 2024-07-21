# How Incremental Builds Work in C

Take a look at the testintmath program shown below. We'll use this as a running example throughout this chapter, demonstrating how incremental builds work.&#x20;

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


Recall the underlying process by which `testinmath` is built.  The source files `intmath.c` and `testintmath.c` are _independently_ preprocessed, compiled, and assembled into object files `intmath.o` and `testintmath.o`, respectively. Of note is that in the preprocessing stage, headers specified via the `#include` directive are fetched and inserted into each file. To produce the executable `testintmath`, `intmath.o` and `testintmath.o` are linked--along with necessary object files from the C standard library. This multi-stage process is summarized in Figure X.

<figure><img src="../.gitbook/assets/Frame 31 (2).png" alt=""><figcaption></figcaption></figure>

The key to incremental builds lies in caching object files and reusing them in subsequent builds when the source files they are derived from, or _depend_ on, haven't changed. Notice that each object file depends on its corresponding `.c` file and `#included` headers. Specifically:

- testintmath.o depends on testintmath.c, stdio.h, stdlib.h, and intmath.h 
- intmath.o depends on intmath.c and intmath.h 

In practice, we need not be concerned with stdio.h and stdlib.h, since these are system headers that we dont modify. therefore, we'll ignore them going forward. 

In practice, this means that if we modify only `testintmath.c`, we can rebuild our program by rebuilding `testintmath.o` and linking it with the existing `intmath.o`. Similarly, if we modify only `intmath.c`, we can rebuild our program by rebuilding `intmath.o` and linking it with the existing `testintmath.o`. Let’s demonstrate this incremental build strategy in action.

The first time we build `testintmath`, a full build is required; there’s no way around that. Importantly, however, we ensure to save the intermediately generated object files--`intmath.o` and `testintmath.o`--which by default `gcc` discards. How do we save object files? Recall the `-c` option, which tells `gcc` to halt the build process after the assembly stage and output object files. Thus, we build `testintmath` with the following two commands:

```
gcc -c intmath.c testintmath.c
gcc intmath.o testintmath.o -o testintmath
```

With the object files in hand, subsequent builds can be incremental. For example, suppose we modify `intmath.c`. To rebuild `testintmath`, we run `gcc -c` on `intmath.c` **only**, and then we link the newly created `intmath.o` with `testintmath.o` from the previous build:

```
gcc -c intmath.c
gcc intmath.o testintmath.o -o testintmath
```

This process is summarized in Figure X.

<figure><img src="../.gitbook/assets/Frame 34.png" alt=""><figcaption></figcaption></figure>

Similarly, suppose we modify `testintmath.c`. To rebuild `testintmath`, we run `gcc -c` on `testintmath.c` only, and then we link the newly created `testintmath.o` with `intmath.o` from the previous build:

```
gcc -c testintmath.c
gcc intmath.o testintmath.o -o testintmath
```

Suppose, however, that we were to modify `intmath.h`. This renders both `intmath.o` and `testintmath.o` obsolete, since `intmath.h` is #included in both their source files. As such, a full rebuild is required:

```
gcc -c intmath.c testintmath.c
gcc intmath.o testintmath.o -o testintmath
```

In general, changes to header file tend to be much more dramatic than changes to `.c` files, since header files, which serve as interfaces, are typically included in many `.c` files. For this reason, great caution should be taken before modifying a header file.

{% hint style="info" %}
It's important to understand that fundamentally, the underlying GCC build process is the same irrespective of whether we build our program via two commands:

```bash
gcc -c intmath.c testintmath.c
gcc intmath.o testintmath.o -o testintmath
```

Or via a single command:

```bash
gcc intmath.c testintmath.c -o testintmath
```

In both cases, `intmath.c` and `testintmath.c` will be independently preprocessed, compiled, and assembled into object files, which are then linked. The difference between these two approaches is that the two-command approach retains the object files while the single-command approach does not.
{% endhint %}
