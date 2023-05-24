# Code Reusability



```c
#include <stdio.h>

int main() {
    printf("Hello, World!\n");
    return 0; 
}
```





## Function Prototype&#x20;

The function prototype for printf() is:

```c
int printf(const char *format, ...);
```

The compiler uses the function prototype for type checking.

## Preprocessing and Header Files

The printf() prototype resides in a stdio.h file, a _header file_ with declarations for standard input and output functions. Before the compilation phase, the content of the stdio.h file are imported into the hello.c program during the preprocessing phase using the #include preprocessor directive.



## User-defined Header Files&#x20;

Header files are not only limited to predefined library functions.&#x20;

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

##
