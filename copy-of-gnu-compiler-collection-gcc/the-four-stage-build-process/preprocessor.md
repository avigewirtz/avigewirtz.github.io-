# Preprocessing Stage

In the first stage of the build process, gcc sends testcircle.e and circle.c to the C preprocessor. The C preprocessor is a program which modifies their source code in testcircle.c and circle.c before actual compilation begins. It does two main things:

1. The preprocessor removes comments from the source code, replacing each one with a single space. Comments are useful for humans, but serve no purpose for the compiler; hence they are discarded.
2. Handles _preprocessor directives._ Preprocessor directives are lines in the C source code whose first (nonblank) character is a `#` (hash). They serve as instructions to the preprocessor to perform various tasks. testcircle.c and circle.c contain two types of preprocessor directives: #include, and #define.&#x20;

### #include directive

The `#include` directive instructs the preprocessor to "include" the contents of the specified file in the location where the directive appears. For example, in `testcircle.c`, the preprocessor replaces `#include <stdio.h>` with the contents of `stdio.h`, which is a system header file containing declarations for functions like `printf()` and `scanf()`.

{% hint style="info" %}
There are two variants of the `#include` directive: with angle brackets (e.g., `#include <stdio.h>`), and with double quotes (e.g., `#include "circle.h"`). The difference between these two has to do with how the preprocessor searches for the referenced file, with the precise details being implementation-defined. All you need to know is to use angle brackets for system header files and double quotes for your own header files.&#x20;
{% endhint %}

### #define directive

The #define directive creates a preprocessor macro, which is essentially an alias for a specific value or code snippet. Whenever the macro name is used in the code, the preprocessor replaces it with the macro's value. In circle.c, `#define PI 3.14159` creates the macro PI and assigns it the value 3.14159. When PI is subsequently used in circle.c, the preprocessor replaces it with 3.14159.&#x20;

## testcircle.c/circle.c vs. testcircle.i/circle.i

Let's now examine the precise modifications the preprocessor makes to our program by comparing the .c and .i versions of our program. \<fill in>

<figure><img src="../../.gitbook/assets/Group 19 (4).png" alt=""><figcaption></figcaption></figure>

*
* First, we see that all comments from circle.c and testcircle.c were removed.
* testcircle.i contains the contents of stdio.h, stdlib.h, and circle.h in the place where their respective #include directives apeared. Similarly, circle.i contains the contents of circle.h. Note that the entire contents of stdio.h and stdlib.h are inserted, though for clarity and space constraints, testcircle.i only shows the relevant parts.&#x20;
* PI from circle.c is replaced with "3.14159". EXIT\_FAILURE is replaced with 1. The EXIT\_FAILURE macro is defined in stdlib.h.&#x20;

## &#x20;Function declarations





























{% hint style="info" %}
* The preprocessor was not originally part of C language. Added in 1973&#x20;
{% endhint %}

### Conditional compilation

Conditional compilation is a technique whereby you can omit entire segments of code from the translation unit sent by the preprocessor to the compiler. Preprocessor directives that control conditional compilation are known as conditional directives. Conditional directives all begin with #if, and they must be terminated by an #endif. This segment of text enclosed within the conditional directives is called controlled text.&#x20;

In circle.h, we wrap all the contents in conditional directives to prevent it from being included twice in the same translation unit. For reference, here is the relevant code, with the controlled text highlighted in red:

\#ifndef CIRCLE\_H

\#define CIRCLE\_H

double calculateRadius(double circumference);&#x20;
