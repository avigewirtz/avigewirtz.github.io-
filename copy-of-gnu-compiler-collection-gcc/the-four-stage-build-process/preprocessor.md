# Preprocessing Stage

The C preprocessor is a program which modifies their source code in testcircle.c and circle.c before actual compilation begins. Its output is stored in testcircle.i and circle.i, which are fed to the compiler. The preprocessor does two main things:

1. Removes comments from the source code, replacing each one with a single space. Comments are useful for humans, but serve no purpose for the compiler; hence they can be discarded.
2. Handles _preprocessor directives._ Preprocessor directives are lines in the C source code whose first (nonblank) character is a `#` (hash). They serve as instructions to the preprocessor to perform various tasks. testcircle.c and circle.c contain two types of preprocessor directives: `#include`, and `#define`.&#x20;

### #include directive

The `#include` directive instructs the preprocessor to "include" the contents of the specified file in the location where the directive appears. For example, `#include <stdio.h>` in testcircle.c instructs the preprocessor to insert the contents of _stdio.h_ in the place where the directive appears. _stdio.h_ is a system header file which contains declarations of functions like `printf()` and `scanf()`.

{% hint style="info" %}
There are two variants of the `#include` directive: with angle brackets (e.g., `#include <stdio.h>`), and with double quotes (e.g., `#include "circle.h"`). The difference between these two has to do with how the preprocessor searches for the specified file, with the precise details being implementation-defined. All you need to know is to use angle brackets for system header files and double quotes for your own header files.&#x20;
{% endhint %}

### #define directive

The #define directive creates a preprocessor macro, which is essentially an alias for a specific value or code snippet. Whenever the macro name is used in the code, the preprocessor replaces it with the macro's value. In circle.c, for example, `#define PI 3.14159` creates the macro `PI` and assigns it the value `3.14159`.  Whenever `PI` is subsequently encountered by the preprocessor in circle.c, it will be replaced with `3.14159`.&#x20;

## Examining preprocessed files

Let's now examine the precise modifications the preprocessor made to our program by inspecting testcircle.i and circle.i and comparing them to testcircl.c and circle.c.&#x20;

<figure><img src="../../.gitbook/assets/Group 19 (4).png" alt=""><figcaption></figcaption></figure>

* **Comments Removal.** First, we see that testcircle.i and circle.i do not contain comments. All comments in circle.c and testcircle.c were removed.
* **File Inclusion**. Second, we see that the preprocessor fetched the header files specified via #include directives in testcircle.c and circle.c and added their contents in the place where their their include directives appeared. In testcircle.i, we see the contents of the stdio.h, stdlib.h, and circle.h in the place where their directives appeared. Note that stdio and stdlib.h are large files, so we only show the relevant parts. For circle.c, the preprocessor inserted contents of circle.h.&#x20;
* **Macro expansion**. Finally, we see that all macros have been expanded. PI in circle.c was replaced with 3.14159, and EXIT\_FAILURE in testcircle.c was replaced with 1. EXIT\_FAILURE is a macro defined in stdlib.h,  from circle.c is replaced with "3.14159". EXIT\_FAILURE is replaced with 1. The EXIT\_FAILURE macro is defined in stdlib.h.&#x20;

## &#x20;Function declarations



### Conditional compilation

Conditional compilation is a technique whereby you can omit entire segments of code from the translation unit sent by the preprocessor to the compiler. Preprocessor directives that control conditional compilation are known as conditional directives. Conditional directives all begin with #if, and they must be terminated by an #endif. This segment of text enclosed within the conditional directives is called controlled text.&#x20;

In circle.h, we wrap all the contents in conditional directives to prevent it from being included twice in the same translation unit. For reference, here is the relevant code, with the controlled text highlighted in red:

\#ifndef CIRCLE\_H

\#define CIRCLE\_H

double calculateRadius(double circumference);&#x20;
