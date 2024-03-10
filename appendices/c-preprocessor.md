# C Preprocessor

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
