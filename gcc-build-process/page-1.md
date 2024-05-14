# Example

Let's now analyze each of the build stages in practice. We'll use the multi-file C program shown below as an example.&#x20;

{% tabs %}
{% tab title="testcircle.c (client)" %}
{% code lineNumbers="true" %}
```c
/*--------------------------------------------------------------------*/
/* testcircle.c                                                       */
/*                                                                    */
/* Calculates the area of a circle given its radius.                  */
/*--------------------------------------------------------------------*/
 
#include <stdio.h>
#include <stdlib.h>
#include "circle.h"

/* Prompts user for the radius of a circle. Returns
   EXIT_FAILURE if input is invalid. Otherwise, prints
   circle's area to stdout and returns 0. */
   
int main(void) {

  double radius, area;

  printf("Enter radius of circle: ");
  if (scanf("%lf", &radius) != 1 || radius <= 0) {
    printf("Invalid input. Must be a positive number.\n");
    exit(EXIT_FAILURE);
  }

  area = calculateArea(radius);

  printf("The area of the circle is: %.2f\n", area);

  return 0;
}
```
{% endcode %}
{% endtab %}

{% tab title="circle.c (implementation)" %}
{% code lineNumbers="true" %}
```c
/*--------------------------------------------------------------------*/
/* circle.c                                                           */
/*--------------------------------------------------------------------*/

#include "circle.h"
#define PI 3.14159

double calculateArea(double radius) {
    return PI * radius * radius;
}
```
{% endcode %}
{% endtab %}

{% tab title="circle.h (interface)" %}
{% code lineNumbers="true" %}
```c
#ifndef CIRCLE_H
#define CIRCLE_H

double calculateArea(double radius);

#endif
```
{% endcode %}
{% endtab %}
{% endtabs %}

We'll build our program using the `--save-temps` option:

```
gcc217 --save-temps intmath.c testintmath.c -o testintmath
```

## Preprocessing Stage

As we mentioned earlier, the preprocessor performs two main tasks: It removes comments, which are of no use to the compiler, and handles preprocessor directives, which are lines in the code that begin with a #. Our program makes use of three types of preprocessor directives: `#include`, `#define`, and `#ifndef`/ `#endif`. These directives control file inclusion, macro definition, and conditional compilation respectively.

#### File Inclusion

The `#include` directive instructs the preprocessor to grab the contents of a specified file and paste it directly into the current file where the `#include` directive appears. For example, in `testcircle.c`, the preprocessor replaces `#include <stdio.h>` with the contents of `stdio.h`, a system header file that contains, among other things, declarations of standard I/O functions such as `printf` and `scanf`.

{% hint style="info" %}
`#included` files are typically header files, but technically any file can be included.
{% endhint %}

{% hint style="info" %}
There are two syntaxes for the `#include` directive: with angle brackets (e.g., `#include <stdio.h>`), and with double quotes (e.g., `#include "circle.h"`). The difference between these two lies in how the preprocessor searches for the specified file, with the precise details being implementation-defined. In general, files included with angle brackets are searched for in system directories only, while those included with double quotes are searched for in the working directory first.
{% endhint %}

#### Macro Definition

The `#define` directive creates a preprocessor macro, which is essentially an alias for a specific value or code snippet. In circle.c, for example, `#define PI 3.14159` creates the macro `PI` and assigns it the value `3.14159`. Whenever `PI` is subsequently used in `circle.c`, the preprocessor replaces it with `3.14159`.

#### Conditional Compilation

The `#ifndef` / `#else` directives, which we use in `intmath.h`, are part of a set of directives known as _conditional_ _directives_. These are used to control which parts of the source code are sent to the compiler. One of their most common use cases is to prevent the contents of a header file from being included twice in the same compilation unit (i.e., `.i` file). This technique is known as an _#include guard_. Here's how it works in `intmath.h`:

* `#ifndef CIRCLE_H`: This checks if the macro `CIRCLE_H` is defined. If this evaluates to TRUE (i.e., `CIRCLE_H` is not defined), the preprocessor continues to process the code between `#ifndef` and `#endif`. If it evaluates to FALSE, the preprocessor skips the entire block within the `#ifndef` ... `#endif`.
* `#define CIRCLE_H`: This defines `CIRCLE_H`. Notice that it doesn't give CIRCLE\_H. Any specific value. That is fine.&#x20;
* `#endif`: This line ends the conditional preprocessor directive started by `#ifndef`.&#x20;

#### Examining `testcircle.i` and `circle.i`

You can examine the preprocessed files with a text editor. Let’s examine `testcircle.i` and `circle.i` to see what precisely was done by the preprocessor. A side-by-side comparison is shown in Figure 12.

<figure><img src="../.gitbook/assets/Group 19 (5).png" alt=""><figcaption></figcaption></figure>

First, we see that the preprocessor removed all comments from `testcircle.c` and `circle.c`. Second, it replaced each `#include` directive with the contents of its specified header: `circle.h` for both `circle.c` and `testcircle.c`, and `stdio.h` and `stdlib.h` for `testcircle.c`. The `stdio.h` file contains declarations for the `printf` and `scanf` functions, while `stdlib.h` includes the declaration for the `exit` function and the definition of the `EXIT_FAILURE` macro. Finally, all macros were expanded: `PI` in `circle.c` was replaced with `3.14159`, and `EXIT_FAILURE` was replaced with `1`.

{% hint style="success" %}
You can think of the preprocessor as a "search-and-replace" tool:

* It replaces each comment with a whitespace character.
* It replaces each `#include` directive with the contents of the specified file.
* It replaces each macro with its value.
{% endhint %}

### Compilation Stage&#x20;

The next stage of the build process is where actual compilation takes place. In this stage, the preprocessed C code in circle.i and testcircle.i is translated into assembly language, stored in circle.s and testcircle.s (Figure 12). The specific assembly language it gets translated top depends on the target processor. On Armlab, which&#x20;

<div align="center">

<figure><img src="../.gitbook/assets/Group 30 (1).png" alt="" width="563"><figcaption></figcaption></figure>

</div>

#### Characteristics of Assembly Language

Detailed coverage of assembly language is beyond the scope of this chapter. ARM64 assembly will be covered in detail in the second half of the course. For now, we will simply provide a few general points about assembly:

* **Extremely Low-Level Language.** Essentially, a human-readable version of the target processor's machine language. There is typically a one-to-one mapping between an assembly language instruction and a machine language instruction.
* **Specific to Target Architecture:** Each architecture has its own assembly language.
* **Not Portable:** Unlike a high level language like C that can be  that can be easily translated into  In simple terms, this means that if I gave you an assembly language program written for an architecture like x86 and told you to run it on an architecture like ARM, you'd have a very hard time doing so.

## Assembly Stage

The assembler translates the assembly-language in testcircle.s and circle.s into machine language, storing the results in testcircle.o and circle.o. This process is shown in Figure 4.3. Machine language is a binary language, consisting of only two symbols--0 and 1.

<figure><img src="../.gitbook/assets/Group 31.png" alt="" width="563"><figcaption></figcaption></figure>

* machine language&#x20;
* testcircle.o missing definitions of printf, scanf, exit, and area

## Linking Stage

* entry symbol \_start

At this point, we have two object files--circle.o and testcircle.o. These files both contain machine code, but they are not executable. circle.o has an undefined reference to \`main'. And testcircle.o has undefined references to four functions: calculateArea, exit, printf, and scanf.&#x20;

In the final stage, tescircle.o and circle.o get sent to the linker. The linker linker combines all these files--testcircle.o, circle.o, and C library--together, resolving all external references in our program. The output is a single file--the executable testcircle. This process is shown in Figure 6.&#x20;

{% hint style="info" %}
should mention starter code role of linker as aside
{% endhint %}



<figure><img src="../.gitbook/assets/Group 49 (2).png" alt="" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
Throughout this chapter, we assumed static linking. Another texhbuique known as dynamic linking is also used, where library functions are linked during runtime, not during the build process.&#x20;
{% endhint %}
