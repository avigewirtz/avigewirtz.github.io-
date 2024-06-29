# Incremental Builds

Suppose we have the equation $$z=sin(x) + cos(y)$$, where $$x=37^∘$$and $$y=73^∘$$. To compute $$z$$, we first calculate $$sin(37^∘)$$, which is approximately $$0.6018$$. Next, we calculate $$cos(73^∘)$$, which is approximately $$0.2924$$. Adding these together, we get $$z=0.6018 + 0.2924 = 0.8942$$.

Now, suppose 𝑦 changes from $$y=73^∘$$ to $$y=83^∘$$. To recompute 𝑧, we don’t need to recompute  $$sin(37^∘)$$. We can reuse $$0.6018$$ from our previous calculation--provided we saved it, that is! The only new nontrivial computation needed is $$cos(83^∘)$$, which is approximately $$0.1219$$. So now,   $$z=0.6018 + 0.1219 = 0.7237$$.

What does this have to do with C programs? Well, the principles of incremental builds in C work in exactly the same way. Recall the process by which multi-file programs are built. Each `.c` file is _independently_ preprocessed, compiled, and assembled into an object file. For sinplicity, we'll refer to this process as compilation, but keep in mind that we actaully mean preprocessing, compilation, and assembly. Of note is that in the preprocessing stage, the headers specified in `#include` directives are inserted into the file. Then, the object files are combined--along with along with necessary object files from the C standard library--to produce an executable file. This process is shown is Figure 12.&#x20;

<figure><img src="../.gitbook/assets/Frame 32.png" alt="" width="563"><figcaption></figcaption></figure>

Notice that each object file is derived only from it's corresponding .c file and included headers. It is not derived from any other source files. Applying the principles of incremental builds, after the source code is modified, only the affected object files need to be rebuilt. Then, you link the updated object files with the "old" object files from previous builds--provided you saved them, of course--to produce an updated executable.&#x20;

We can summarize the incremental build strategy as follows:

* The first time you build your program, build the entire thing; however, ensure to save the object files.&#x20;
* In subsequent builds, rebuild only the affected object files. Then, link them with the "old" object files to produce an updated executable.&#x20;

#### Example

Let's demonstrate incremental builds in action. As an example, we'll use the testintmath program from precept four.&#x20;

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

The first time we build testintmath, we build the entire program, but we ensure to save objevct files. How do we save object files? Recall the -c option, which tells gcc to halt after the assembly stage and output object files.&#x20;

```
gcc -c intmath.c testintmath.c
gcc intmath.o testintmath.o -o testintmath
```

Now suppose we modify intmath.c. We run gcc -c on intmath.c only, then we link the updated intmath.o with the testintmath.o form our previous build.&#x20;

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

#### Challenges of Manually Implementing Incremental Builds

As this example shows, implementing incremental builds manually is possible but it requires some work. In particular, you have to:

1. Keep track of which `.c` and `.h` files were modified since the last build.
2. Know which `.o` files depend on the modified `.c` and `.o` files.

Even for a small program like `testintmath`, this task isn’t particularly fun, though it is admittedly manageable. As programs grow larger, however, and the web of dependencies grows increasingly complex, this task becomes incredibly tedious and error-prone.

Consider a scenario where you modify header file `A`, which is `#included` in, say, 20 `.c` files. You’d have to track down and recompile all these `.c` file. Worse yet, imagine header file `A` is also `#included` in header file `B`. You'd then have to also track down and recompile all the `.c` files that `#include` `B`.

To make life easier (no pun intended), the `make` tool was developed, which automates the process of incremental builds. In the next section, we describe how to use `make`.
