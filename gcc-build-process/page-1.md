# Example

Let's now analyze each of the build stages in practice. As an example, we'll use the multi-file C program shown below.&#x20;

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

### Preprocessing Stage

As we mentioned earlier, the preprocessor performs two main tasks: It removes comments, which are of no use to the compiler, and handles preprocessor directives, which are lines in the code that begin with a `#`. Our program makes use of three types of preprocessor directives: `#include`, `#define`, and `#ifndef`/ `#endif`. These directives control file inclusion, macro definition, and conditional compilation respectively.

#### File Inclusion

The `#include filename` directive instructs the preprocessor to grab the contents of the specified file and paste it directly into the current file where the `#include` directive appears. For example, in `testcircle.c`, the preprocessor replaces `#include <stdio.h>` with the contents of `stdio.h`. `#included` files are typically header files, but technically any file can be included.

{% hint style="info" %}
Notice that there are two syntaxes for the `#include` directive: with angle brackets (e.g., `#include <stdio.h>`), and with double quotes (e.g., `#include "circle.h"`). The difference between these two lies in how the preprocessor searches for the specified file, with the precise details being implementation-defined. In general, files included with angle brackets are searched for in system directories only, while those included with double quotes are searched for in the working directory first and then the system directories.&#x20;
{% endhint %}

#### Macro Definition

The `#define` directive creates a preprocessor macro, which is essentially an alias for a specific value or code snippet. In `circle.c`,  `#define PI 3.14159` creates the macro `PI` and assigns it the value `3.14159`. Whenever `PI` is subsequently used in `circle.c`, the preprocessor replaces it with `3.14159`.

In `testcircle.c`, we use the `EXIT_FAILURE` macro, which is defined in `exit.h`.

{% hint style="info" %}
**Predefined Macros**


{% endhint %}

#### Conditional Compilation

The `#ifndef` / `#else` directives, which we use in `intmath.h`, are part of a set of directives known as _conditional_ directives. These are used to control which parts of the source code are sent to the compiler. One of their most common use cases is to prevent the contents of a header file from being included twice in the same compilation unit (i.e., `.i` file). This technique is known as an _#include guard_. Here's how it works in `intmath.h`:

* `#ifndef CIRCLE_H`: This checks if the macro `CIRCLE_H` is defined. If this evaluates to TRUE (i.e., `CIRCLE_H` is not defined), the preprocessor continues to process the code between `#ifndef` and `#endif`. If it evaluates to FALSE, the preprocessor skips the entire block within the `#ifndef` ... `#endif`.
* `#define CIRCLE_H`: This defines `CIRCLE_H`. Notice that it doesn't give `CIRCLE_H` any specific value. This is perfectly valid. The preprocessor will simply note that `CIRCLE_H` is defined.&#x20;
* `#endif`: This line ends the conditional block started by `#ifndef`.&#x20;

#### Examining `testcircle.i` and `circle.i`

Since preprocessed files are text files, you can view them with a text editor, just as you view regular `.c` files. Let’s examine `testcircle.i` and `circle.i` to see what precisely was done by the preprocessor. A side-by-side comparison is shown in Figure 12.

<figure><img src="../.gitbook/assets/Frame 61.png" alt=""><figcaption></figcaption></figure>

First, we see that the preprocessor removed all comments from `testcircle.c` and `circle.c`. Second, it replaced each `#include` directive with the contents of its specified header: `circle.h` for both `circle.c` and `testcircle.c`, and `stdio.h` and `stdlib.h` for `testcircle.c`. The `stdio.h` file contains declarations for the `printf` and `scanf`  functions, while `stdlib.h` contains the declaration for the `exit` function and the definition of the `EXIT_FAILURE` macro. Finally, all macros were expanded: `PI` in `circle.c` was replaced with `3.14159`, and `EXIT_FAILURE` was replaced with `1`.

Each file now contains&#x20;

{% hint style="success" %}
You can think of the preprocessor as a "search-and-replace" tool:

* It replaces each comment with a whitespace character.
* It replaces each `#include` directive with the contents of the specified file.
* It replaces each macro with its value.
{% endhint %}

### Compilation Stage&#x20;

The next stage of the build process is compilation, which is where the bulk of the work takes place. In this stage, `circle.i` and `testcircle.i` are sent to the compiler, which translates them into assembly language files `circle.s` and `testcircle.s`. The specific assembly language depends on the target processor. On Armlab, which uses the ARM64 architecture, the code will be translated into ARM assembly.

<figure><img src="../.gitbook/assets/Frame 63.png" alt="" width="563"><figcaption></figcaption></figure>

**Assembly is basically** a human-readable version of the target processor's machine language. There is typically a one-to-one mapping between an assembly language instruction and a machine language instruction. All characteristics of machine language apply, except it's human readable. There are also assembler macros and labels. We will defer discussion of assembly language until after we cover machine language.&#x20;

### Assembly Stage

The next stage of the build process is assembly. In this stage, `circle.s` and `testcircle.s` are sent to the assembler, which translates them into relocatable object files `circle.o` and `testcircle.o`. These files are essentially machine-code equivalents of `circle.s` and `testcircle.s` (and, by extension, `circle.i` and `testcircle.i` as well).&#x20;

This process is shown in Figure 4.3. Relocatable object files are essentially a machine language representation of their contain Machine language is a binary language, consisting of only two symbols--0 and 1.

<figure><img src="../.gitbook/assets/Frame 62.png" alt="" width="563"><figcaption></figcaption></figure>

#### Characteristics of Machine and Assembly language

Detailed coverage of assembly or machine language is beyond the scope of this chapter. ARM64 assembly will be covered in detail in the second half of the course. For now, we will make a few general points about assembly.&#x20;

* **Assembly is basically** a human-readable version of the target processor's machine language. There is typically a one-to-one mapping between an assembly language instruction and a machine language instruction.&#x20;
* Programmers rarely program in assembly, since compilers can produce code as good as humans. However, still has its place in modern&#x20;
* Not portable. Portability refers to how easy it is to translate a language into the machine language for any arbitrary processor. Portable languages such as C can be translated into the machine into This means that an assembly program written in one language, such as ARM
* Extremely simple. Each instruction does a simple task, such as adding two numbers or moving data from one memory location to another. A single C statement might take several instructions.&#x20;

### Linking Stage

At this point, we have two object files--circle.o and testcircle.o. These files both contain machine code, but they are not executable. circle.o has an undefined reference to \`main'. And testcircle.o has undefined references to four functions: calculateArea, exit, printf, and scanf.&#x20;

In the final stage, tescircle.o and circle.o get sent to the linker. The linker linker combines all these files--testcircle.o, circle.o, and C library--together, resolving all external references in our program. The output is a single file--the executable testcircle. This process is shown in Figure 6.&#x20;

{% hint style="info" %}
should mention starter code role of linker as aside. entry symbol \_start
{% endhint %}

<figure><img src="../.gitbook/assets/Frame 60.png" alt="" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
Throughout this chapter, we assumed static linking. Another texhbuique known as dynamic linking is also used, where library functions are linked during runtime, not during the build process.&#x20;
{% endhint %}

### Rexamining structure of our program

