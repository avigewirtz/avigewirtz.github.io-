# Preprocessing stage

As we mentioned earlier, the preprocessor performs two main tasks: It removes comments, which are of no use to the compiler, and handles preprocessor directives, which are lines in the code that begin with a #. Our program makes use of three types of preprocessor directives, #include, #define, and #ifdef / #else. These directives control file inclusion, macro definition, and conditional compilation.&#x20;

#### File inclusion





1. \#include. This is used to "include" the contents of another file into the current file.  For example, `#include <stdio.h>` tells the preprocessor to insert the contents of the `stdio.h`. stdio.h is a C library header file which, among other things, contains declarations of standard I/O functions such as `printf` and `scanf`. As you can imagine, the contents of the #included file get inserted in the place where the directive appears.&#x20;
2. \#define&#x20;
3. \#ifdef / #else

{% hint style="info" %}
You can think of the preprocessor as a "seach-and-replace" tool:

* It replaces each comment with a whitespace character
* It replaces each #include directive with the contents of the specified file
* It replaces each macro with its value
{% endhint %}

The output of the preprocessor is essentially raw C code. No comments.&#x20;

You can examine the output of the preprocessor with a text editor. An

<figure><img src="../../.gitbook/assets/Group 19 (5).png" alt=""><figcaption></figcaption></figure>

Frst, we see that the preprocessor removed all comments from testcircle.c and circle.c. Second, we see that each #include directive was replaced with the contents of its specified header. Namely, circle.h for circle.c and testcircle.c, and stdio.h and stdlib.h for testcircle.h. stdio.h and stdlib.h are system header files, containing declarations of library functions and definitions of macros. stdio.h contains the declaration of printf and scanf, and stdlib contains the declaration of exit and the the definition of the EXIT\_FAILURE macro. Finally, we see that all macros were expanded. PI in circle.,c was replaced with 3.14159, and EXIT\_FAILURE was replaced with 1.&#x20;



{% hint style="info" %}
Note: The preprocessor actaully performs a lot more work then shown here. The full task of the preprocessor is stages 1-4 of the compilation stages outlined by the C standard.&#x20;
{% endhint %}



Difference is that .c files contain code in the preprocessing laguage. Preprocessing language can be thought of as a subset of the C language.&#x20;

Critical to understand that input to preprocessor is C code, and output is also C code. The difference is that&#x20;



## Conditional compilation

## role of header files



















The preprocessor does two main things:

1. Removes comments from the source code, replacing each one with a single space. Comments are useful for humans, but serve no purpose for the compiler; hence they can be discarded.
2. Handles _preprocessor directives._ Preprocessor directives are lines in the C source code whose first (nonblank) character is a `#` (hash). They serve as instructions to the preprocessor to perform various tasks. testcircle.c and circle.c contain two types of preprocessor directives: `#include`, and `#define`.&#x20;

### #include directive

The `#include` directive inserts the contents of the specified file in the location where the directive appears. In testcircle.c, for example, the preprocessor inserts the contents of stdio.h in the place where `#include <stdio.h>` appears. _stdio.h_ is a system header file which contains the prototypes of functions like `printf()` and `scanf()`.

{% hint style="info" %}
There are two variants of the `#include` directive: with angle brackets (e.g., `#include <stdio.h>`), and with double quotes (e.g., `#include "circle.h"`). The difference between these two has to do with how the preprocessor searches for the specified file, with the precise details being implementation-defined.&#x20;
{% endhint %}

### #define directive

The #define directive creates a preprocessor macro, which is essentially an alias for a specific value or code snippet. Whenever the macro name is used in the code, the preprocessor replaces it with the macro's value. In circle.c, for example, `#define PI 3.14159` creates the macro `PI` and assigns it the value `3.14159`.  Whenever `PI` is subsequently used in circle.c, the preprocessor replaces it with `3.14159`.&#x20;

### Conditional compilation

Conditional compilation is a technique whereby you can omit entire segments of code from the translation unit sent by the preprocessor to the compiler. Preprocessor directives that control conditional compilation are known as conditional directives. Conditional directives all begin with #if, and they must be terminated by an #endif. This segment of text enclosed within the conditional directives is called controlled text.&#x20;

In circle.h, we wrap all the contents in conditional directives to prevent it from being included twice in the same translation unit. For reference, here is the relevant code, with the controlled text highlighted in red:

\#ifndef CIRCLE\_H

\#define CIRCLE\_H

double calculateRadius(double circumference);&#x20;
