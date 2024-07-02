# Incremental Builds

Suppose we have the equation $$z = \sin(x) + \sin(y)$$, where $$x = 37^\circ$$ and $$y = 73^\circ$$. To compute $$z$$, we first calculate $$\sin(37^\circ)$$, which is approximately $$0.6018$$. Next, we calculate $$\sin(73^\circ)$$, which is approximately $$0.9563$$. Adding these together, we get $$z = 0.6018 + 0.9563 = 1.5581$$.

Now, suppose 𝑦 changes from $$y = 73^\circ$$ to $$y = 83^\circ$$. To recompute 𝑧, we don’t need to recompute $$\sin(37^\circ)$$. We can reuse the $$0.6018$$ value we obtained in our previous computation--provided we saved it, that is! The only new nontrivial computation needed is $$\sin(83^\circ)$$, which is approximately $$0.9925$$. So now, $$z = 0.6018 + 0.9925 = 1.5943$$.

What does this have to do with C programs? Well, the principle of incremental builds in C work in exactly the same way. Recall the process by which multi-file programs are built. First, each `.c` file is _independently_ translated into an object file. For simplicity, we'll refer to this process as compilation, but keep in mind that we actually mean preprocessing, compilation, and assembly. Of note is that in the preprocessing stage, headers specified in `#include` directives are inserted. Then, to produce an executable, the object files are linked--along with necessary object files from the C standard library. This process is shown in Figure 12 using a dummy foobar program.

<figure><img src="../.gitbook/assets/Frame 32.png" alt="" width="563"><figcaption></figcaption></figure>


We can model this process using the following equation:

foobar = compile(foo.c) + compile(bar.c)

Of course, linking or more complicated than the simple concatenation of object files, but this equation will do. 

Just like in our math example, when y changed we didnt need to recomouter sin(x), so too when a .c file such as foo.c changes, we dont need to recompile bar.c. We recompile foo.c alone, and then we link foo.o with bar.o, producing an uodated foobar. 

The caveat is that diving a C program in terms of .c files is an oversimplification, since .c files can #include .h files. Thus, we really need to think in terms of a .c file, along woth all .h files incoided in it. This is known as a transaltion unit. Thus, we really need to think in terms of translation units. Also note than transaltion units can iverlap. For example, suppose foo.c and bar.c both #include foo.h. Then foo.h is a part of two trabsaltion units. 
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

The first time we build testintmath, we compile all source files, but we ensure to save object files. How do we save object files? Recall the -c option, which tells gcc to halt after the assembly stage and output object files.

```
gcc -c intmath.c testintmath.c
gcc intmath.o testintmath.o -o testintmath
```

Now suppose we modify intmath.c. To rebuild testintmath, we run gcc -c on intmath.c only. Then, we link the resulting intmath.o with the testintmath.o form our previous build.

```
gcc -c intmath.c
gcc intmath.o testintmath.o -o testintmath
```

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

Fundamentally, the only difference between these two approaches is that the two-command approach retains the`.o` files while the single-command approach does not.
{% endhint %}
