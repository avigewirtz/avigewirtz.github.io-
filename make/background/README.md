# Background

The beauty of `make` lies in its ability to combine the efficiency benefits of compiling only what is necessary with the convenience of not having to manually track which parts of the codebase have changed.

## Motivation for Make

As multi-file C programs grow larger, the compilation process becomes more complex. The traditional method of recompiling all source files whenever a modification to the codebase is introduced becomes inefficient or even impractical due to increased build times and resource consumption. This is where taking advantage of GCC's feature of separate compilation comes into play.

Separate compilation is the practice of compiling each source file of a project as a separate unit into something called an object file and then linking the object files together to create an executable. The advantage of this approach is that when a change is made to a part of the codebase, only the affected source files need to be recompiled, not the entire project.

&#x20;if a change is introduced to a source file, then only only the source files whose corresponding object file would be affected by the change need to be recompiled. Source files that are&#x20;

Let's demonstrate the idea of separate compilation with a simple program, consisting of three files: `intmath.c`, `testintmath.c`, and `intmath.h`. `intmath.c` contains the implementation of two functions, `gcd` (greatest common divisor) and `lcm` (least common multiple).`testintmath.c` contains the `main` function, which tests these two functions by prompting the user for two integers, passing them to the gcd and lcm functions in intmath.c, and displaying the results. The `intmath.h` file contains declarations of the `gcd` and `lcm` functions, ensuring that the types of the arguments and return value match up correctly between the function call and the function definition.

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

To compile the program, we invoke gcc217 with both intmath.c and testintmath.c as arguments. Note that we need not include intmath.h in the list of files specified, since it is automatically included in the appropriate points with the #include directive.&#x20;

<pre class="language-bash"><code class="lang-bash"><a data-footnote-ref href="#user-content-fn-1">gcc217 intmath.c testintmath.c -o intmath</a>
</code></pre>

This will result in an executable named intmath, which we can run by invoking its pathname. Let's examine what took place behind the scenes when we invoked the gcc command.&#x20;

<figure><img src="../../.gitbook/assets/Group 65-3.png" alt="" width="563"><figcaption></figcaption></figure>

* rather than compile intmath.c and testintmath.c as a monolith--that is, rather than combine the source code of intmath.c and testintmath.c into a single unit and then compile the single unit--GCC compiles intmath.c and testintmath.c independently.  each into an object file, named intmath.o and testintmath.o, respectively. These object files contain machine code, but they are not executable. testintmath.o is not executable since it contains references to four external functions--gcd and lcm, whose implementation is in intmath.o, and printf and scanf, from the C Standard Library. Similarly, intmath.o is not executable, since it does not contain a main method.&#x20;
* To generate an executable, GCC merges testintmath.o, intmath.o, as well as the relevant library code, resolving all external references. The result is an executable file named intmath.&#x20;
*

[^1]: Note that the header file ‘intmath.h’ is not specified in the list of files on the command line, since it is automatically included in appropriate points by the #include directives in ‘intmath.c’ and ‘testintmath.c’.&#x20;
