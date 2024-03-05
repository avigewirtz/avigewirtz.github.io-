# Preprocessing Stage

* The preprocessor performs a series of textual transformations on its input. These happen before all other processing.

In the first stage of the build process, gcc sends testcircle.e and circle.c to the C preprocessor. The C preprocessor is a program  which modifies their source code in testcircle.c and circle.c before actual compilation begins. It does two main things:

1. Removes comments from source code. Comments are useful for humans, but add nothing but overhead for the compiler; hence, they are discarded. All comments are replaced with single spaces. Line comments are not in the 1989 edition of the C standard, but they are recognized by GCC as an extension.
2. Handles _preprocessor directives._ Preprocessor directives are lines in the C source code whose first (nonblank) character is a `#` (hash). They serve as instructions to the preprocessor to perform various tasks. testcircle.c and circle.c contain two types of preprocessor directives: #include, and #define.&#x20;

### #include directive

The `#include` directive instructs the preprocessor to "include" the contents of the specified file in the place where the include directive appears. In testcircle.c, for example, the preprocessor replaces `#include <stdio.h>` with the contents of _stdio.h_. stdio.h is a system header file which contains, among other things, declarations of the printf() and scanf() functions.&#x20;

{% hint style="info" %}
There are two variants of the `#include` directive: with angle brackets (e.g., `#include <stdio.h>`), and with double quotes (e.g., `#include "circle.h"`). The difference between these two has to do with how the preprocessor searches for the referenced file, with the precise details being implementation-defined. All you need to know is to use the angle brackets variant for system header files and the double quotes variant for your own header files.&#x20;
{% endhint %}

### #define directive

The #define directive is used to create a preprocessor macro. A macro is essentially an alias for an arbitrary sequence&#x20;

In circle.c, for example, the preprocessor replaces all occurrences of PI with 3.14159.&#x20;



## testcircle.c/circle.c vs. testcircle.i/circle.i

Let's now examine the difference&#x20;

&#x20;

<figure><img src="../../.gitbook/assets/Group 19 (2).png" alt=""><figcaption><p>Figure 2: Comparision of tescircle.c/circle.c with testcircle.i/circle.i. (Click to enlarge). </p></figcaption></figure>

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
