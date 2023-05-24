# Dependencies

You'd be hard pressed to find a self contained C program. Virtually everyone contains references to other files. essentially dependent on them in order to run. for example, consider the following program, main.c:

```c
#include "example.h"
#include <stdio.h>

void print_point(Point p) {
    printf("Point: (%d, %d)\n", p.x, p.y);
}

int main() {
    Point p; 
    p.x = 5;
    p.y = 10;

    print_point(p);
    
    double area = PI * p.x * p.x;
    printf("The area of a circle with radius %d is %.2f\n", p.x, area);

    return 0;
}
```

Here are the dependencies:



* Point
* PI
* printf&#x20;



When you compile a C source file, the compiler needs to have certain information:&#x20;

* prototype of each function



```c
#ifndef EXAMPLE_H
#define EXAMPLE_H

#define PI 3.14159

typedef struct {
    int x;
    int y;
} Point;

void print_point(Point p);

#endif 
```

```c
// preprocessed main.c

typedef struct {
    int x;
    int y;
} Point;

void print_point(Point p);

void print_point(Point p) {
    printf("Point: (%d, %d)\n", p.x, p.y);
}

int main() {
    Point p;
    p.x = 5;
    p.y = 10;

    print_point(p);
    
    double area = 3.14159 * p.x * p.x;
    printf("The area of a circle with radius %d is %.2f\n", p.x, area);

    return 0;
}

```



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
