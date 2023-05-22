# Code Reusability

As programmers, we frequently encounter common and repetitive tasks in our different projects. Code reusability, a crucial principle in programming, saves us from rewriting the same code over and over, thereby saving time and minimizing errors. It involves creating code that can be repurposed in various applications.

Programming languages come equipped with an extensive set of predefined functions within libraries. These libraries are collections of beneficial, well-tested, and often-used code that developers can utilize to perform specific tasks without having to build the code from the ground up.

Let's delve into an example to illustrate this concept more clearly.

## Example: The printf Function in C&#x20;

Consider a straightforward C program, hello.c, that prints "Hello, World!" on the standard output (stdout):

```c
#include <stdio.h>

int main() {
    printf("Hello, World!\n");
    return 0; 
}
```

Notice that this program employs the printf() function, even though it isn't explicitly defined within hello.c. Yet, the program operates flawlessly. How is this possible?

Predefined Library Functions The printf() function is a predefined function provided by the C standard library. To make this function available to our program, we need to incorporate the relevant C library.

During the program's linking phase—which follows the assembling phase—the code for the printf() function is imported from the C library into the hello.c program. This process of linking can either be static or dynamic, depending on a variety of factors.

When compiling C programs, GCC necessitates function prototypes to be declared before they are invoked.

## Function Prototype&#x20;

The function prototype for printf() is:

```c
int printf(const char *format, ...);
```

Here's a breakdown of each component:

* int: This signifies the return type of the printf function, which is an integer. It represents the number of characters printed (excluding the null terminator) or a negative value if an error occurs.
* printf: This is the function's name.
* const char \*format: This is the printf function's first parameter, a pointer to a string (char \*) that contains the format specifier and optional format arguments. The 'const' keyword indicates that the function will not alter the string's content.
* ...: This ellipsis signifies the "variable argument list" or "varargs," indicating that printf can accept a variable number of arguments based on the format specifier in the format string.

The compiler uses the function prototype, including the function name, return type, and parameter types, for type checking, code generation, and ensuring correct function usage.

The printf() prototype resides in a stdio.h file, a header file with declarations for standard input and output functions.

## Preprocessing and Header Files

Before the compilation phase, the contents of the stdio.h file are imported into the hello.c program during the preprocessing phase using the #include preprocessor directive.

Header files in C are typically .h files containing C function declarations and macro definitions to be shared across several source files. The #include directive instructs the preprocessor to take all the contents of the specified header file and 'include' them at that specific location in the file being compiled.

## User-defined Header Files&#x20;

Header files are not only limited to predefined library functions. Developers can create their own header files to include user-defined functions.

For instance, we declare a function multiply() in a user-defined header file functions.h:

```c
/* File: functions.h */
#ifndef FUNCTIONS_H
#define FUNCTIONS_H

int multiply(int a, int b);

#endif
```

We can define this function in a separate source file (functions.c):

```c
/* File: functions.c */
#include "functions.h"

int multiply(int a, int b){
    return a * b;
}
```

In any C program where we need the multiply() function, we include our functions.h file and link with functions.c:

```c
#include "functions.h"

int main() {
    int result = multiply(5, 10);
    printf("Result: %d\n", result);
    return 0; 
}
```

## Difference Between System and User-defined Header Files

System and user-defined header files differ mainly in the way they are included in the program.&#x20;

* System Header Files: These files are part of the compiler's standard library and accessed using angle brackets in the #include directive, like #include \<stdio.h>. The compiler has predefined paths set for these files.
* User-defined Header Files: Developers create these header files for their own programs. They are included using double quotes in the #include directive, like #include "functions.h". When quotes are used, the preprocessor searches in the same directory as the file with the #include statement. If it doesn't find it there, it resorts to the directories of the standard system headers.



MACROS
