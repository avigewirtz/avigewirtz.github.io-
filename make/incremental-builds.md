# Incremental Builds

Suppose we have the equation $$z = \sin(x) + \sin(y)$$, where $$x = 37^\circ$$ and $$y = 73^\circ$$. To compute $$z$$, we first calculate $$\sin(37^\circ)$$, which is approximately $$0.6018$$. Next, we calculate $$\sin(73^\circ)$$, which is approximately $$0.9563$$. Adding these together, we get $$z = 0.6018 + 0.9563 = 1.5581$$.

Now, suppose 𝑦 changes from $$y = 73^\circ$$ to $$y = 83^\circ$$. To recompute 𝑧, we don’t need to recompute $$\sin(37^\circ)$$. We can reuse the $$0.6018$$ value we obtained in our previous computation--provided we saved it, that is! The only new nontrivial computation needed is $$\sin(83^\circ)$$, which is approximately $$0.9925$$. So now we have $$z = 0.6018 + 0.9925 = 1.5943$$.

Notice what we did here. We cached the intermediate values generated during the first conputation and reused the unnaffected values in the next computation. What does this have to do with C programs? Well, the principle of incremental builds in C work in exactly the same way. Recall the process by which multi-file programs are built. Each `.c` file is _independently_ preprocessed, compiled, and assembled into an object file. For simplicity, we'll refer to this process as compilation, but keep in mind that we actually mean preprocessing, compilation, and assembly. Of note is that in the preprocessing stage, headers specified in `#include` directives are inserted. Then, to produce an executable, the object files are linked--along with necessary object files from the C standard library. This process is shown in Figure 12 using a dummy `foobar` program.

<figure><img src="../.gitbook/assets/Frame 32.png" alt="" width="563"><figcaption></figcaption></figure>

We can model this process using the following equation:

$$foobar = compile(foo.c) + compile(bar.c)$$

(Of course, linking or more complicated than the simple concatenation of object files, but this equation will do.)&#x20;

We apply the same principle we did in our math example. we cache intermediate reuslts--object files. Then, in future builds, we rebuild only the object files that depend on changed source files.&#x20;



Just like in our math example where only sin(y) was recalculated when `y` changed, so too only compile(foo.c) needs to be re-run when bar.c is modified, and vice versa.&#x20;

The caveat is that diving a C program along the lines of `.c` files is an oversimplification, since `.c` files can `#include` header files. To be more precise, we really need to think it terms of translation units. A translation unit is a .c file along with all headers included. Note that translation units can--and often do--overlap.&#x20;

#### Example

Let's demonstrate incremental builds in action. As an example, we'll use the testintmath program from precept four.

{% tabs %}
{% tab title="testintmath.c" %}
{% code lineNumbers="true" %}
```c
/*--------------------------------------------------------------------*/
/* testintmath.c                                                      */
/* Author: Bob Dondero                                                */
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
/* Author: Bob Dondero                                                */
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
/* Author: Bob Dondero                                                */
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

Our program consists of two translation units.

1. intmath.c and intmath.h
2. testintmath.c, intmafh.h, stdio.h, and stdlib.h

Because stdio.h and stdlib.h are system header files that we do not modify, we won't concern ourselves wirh the.

The first time we build testintmath, we compile all source files, but we ensure to save object files. How do we save object files? Recall the -c option, which tells gcc to halt after the assembly stage and output object files. Thus, we build our program with the following two commands:

```
gcc -c intmath.c testintmath.c
gcc intmath.o testintmath.o -o testintmath
```

Now suppose we modify intmath.c. To rebuild testintmath, we run gcc -c on intmath.c only. Then, we link the resulting intmath.o with the testintmath.o form our previous build.

```
gcc -c intmath.c
gcc intmath.o testintmath.o -o testintmath
```

The process would be the same if we were to modify testintmath.c. Notice, however, that if modify intmath.h, we'd have to recompile both intmath.c and testintmath.c, since they both #include it. Ij general, changes to header files tend to be kuch more dramatic than chnagws to .c files, sincs header files are often part of multiple trabslation units.

{% hint style="info" %}
It's important to understand that the underlying GCC build process is the same irrespective of whether we build our program via two commands:

```bash
gcc217 -c intmath.c testintmath.c
gcc217 intmath.o testintmath.o -o testintmath
```

Or via a single command:

```bash
gcc217 intmath.c testintmath.c -o testintmath
```

In other words, in both cases the .c files will be independently preprocessed, conpiled, and assembled into object files, which are then linked. Fundamentally, the only difference between these two approaches is that the two-command approach retains the object files while the single-command approach does not.
{% endhint %}
