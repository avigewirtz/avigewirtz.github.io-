# Preprocessing Stage

The preprocessor is a program that processes the source files before the bulk of processing--compilation--takes place (hence the name preprocessor). The input is .c files, and the output is .i files.

It does two main things:

1. Removes comments from source code. Comments are useful for humans, but not compiler.
2. Handles _preprocessor directives_

### Preprocessor Directives

Preprocessor directives are lines in our program where the first (nonblank) character is a `#` (hash) symbol. They serve as instructions to the preprocessor to perform various tasks. testcircle.c and circle.c contain two types of preprocessor directives: #include, and #define.&#x20;

### #include directive

The `#include` directive instructs the preprocessor to include the contents of the specified file in the place where the include directive appears. In testcircle.c, for example, the preprocessor replaces `#include <stdio.h>` with the contents of _stdio.h_. stdio.h is a system header file which contains, among other things, declarations of the printf() and scanf() functions.&#x20;

### #define directive

The #define directive is used to create a preprocessor macro.&#x20;

In circle.c, for example, #define PI 3.14159 creates the macro PI, which equals 3.14159.&#x20;

Whenever PI is used in circle.c, the preprocessor will replace it with 3.14159.&#x20;

You can think of it like a variable, but with a few notable differences:&#x20;



<figure><img src="../../.gitbook/assets/Screenshot 2024-03-04 at 11.43.20 AM.png" alt=""><figcaption></figcaption></figure>

































{% hint style="info" %}
* The preprocessor was not originally part of C language. Added in 1973&#x20;
{% endhint %}

### Conditional compilation

Conditional compilation is a technique whereby you can omit entire segments of code from the translation unit sent by the preprocessor to the compiler. Preprocessor directives that control conditional compilation are known as conditional directives. Conditional directives all begin with #if, and they must be terminated by an #endif. This segment of text enclosed within the conditional directives is called controlled text.&#x20;

In circle.h, we wrap all the contents in conditional directives to prevent it from being included twice in the same translation unit. For reference, here is the relevant code, with the controlled text highlighted in red:

\#ifndef CIRCLE\_H

\#define CIRCLE\_H

double calculateRadius(double circumference);&#x20;



### Difference between include syntax

Notice that the syntax for the #include directive differs slightly depending on whether the specified file is a system header file or our header file. For system files, we enclose the filename in <>, such as with #include \<stdio.h> and #include \<stdlib.h> in main.c In contrast, when we include circle.h, which is our own header file we enclose the filename in quotes: #include “circle.h”.&#x20;

###

There are two ways to include files with the `#include` directive: using angle brackets (`#include <filename>`) and using double quotes (`#include "filename"`). The difference between these two has to do with how the compiler searches for the referenced file, with the precise details being implementation-defined. As a general rule, use angle brackets for library headers and double quotes for all other headers.&#x20;
