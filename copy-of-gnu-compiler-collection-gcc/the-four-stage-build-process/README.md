# The Four Stage Build Process

The purpose of compilation is to transform C source code—an English-resembling language suitable for human understanding—into executable machine code—a binary language suitable for computer processing.

GCC performs compilation in four sequential stages: preprocessing, compilation proper, assembly, and linking. We will illustrate the compilation process by following the journey of a C program from source code to executable. The program we will use is a simple program that calculates the area of a circle given its circumference. It consists of three files: main.c, circle.c, and circle.h. Their source code is written below.&#x20;

{% code title="main.c" lineNumbers="true" %}
```c
#include <stdio.h>
#include <stdlib.h>
#include "circle.h"

int main() {
    double circumference, area;

    printf("Enter the circumference of the circle (positive number): ");
    if (scanf("%lf", &circumference) != 1 || circumference <= 0) {
        printf("Invalid input. Circumference must be a positive number.\n");
        exit(EXIT_FAILURE);
    }

    area = calculateArea(circumference);

    printf("The area of the circle is: %.2f\n", area);

    return 0;
}
```
{% endcode %}

{% code title="circle.c" lineNumbers="true" %}
```c
#include "circle.h"
#define PI 3.14159

double calculateArea(double circumference) {
    double radius = circumference / (2 * PI);
    return PI * radius * radius;
}

```
{% endcode %}

{% code title="circle.h" lineNumbers="true" %}
```c
#ifndef CIRCLE_H
#define CIRCLE_H

double calculateArea(double circumference);

#endif
```
{% endcode %}

## Bird’s eye view of the GCC compilation process

Before diving into the complexities of each stage, we'll first give a bird's eye view of the process. Having an overarching view will allow you to grasp the big picture, making it easier to contextualize the more detailed aspects that follow.

* **Preprocessing**: In the first stage, main.c and circle.c are sent to the preprocessor, which is a program that essentially prepares the source files for compilation. It does this by removing comments and responding to preprocessor directives--lines in the code that begin with the # (hash) character. For example, the #include "circle.h" in line 1 of circle.c instructs the preprocessor to insert the contents of the circle.h into... The result of preprocessing is two files: main.i and circle.i. The preprocessor sends main.i and circle.i to the compiler.&#x20;
* **Compilation**: The compiler translates the preprocesses source code in main.i and circle.i to assembly language, which are stored in main.s and circle.s. Assembly language is essentially a human-readable form of the processors machine language.
* **Assembly**: The assembler then converts assembly code in main.s and circle.s to object code, storing the result in main.o and circle.o. Object files are comprised of machine code, but they are not executable, since they may contain external references (such as the call to the calculateArea() function in main.o, which is defined in circle.o) and need not contain a main method (such as circle.o).&#x20;
* **Linking**: The final stage in the compilation process is the linking stage. Here, the linker combines main.o and circle.o, resolving the external reference to calulateArea() in main.o. It also combines the object code for the library code for printf(), scanf(), and exit().  The resulting file is called an executable.&#x20;

This process is summarized in Figure 1.

<figure><img src="../../.gitbook/assets/Group 17.png" alt=""><figcaption></figcaption></figure>

As you can see, the process of transforming our program into an executable resembles an assembly line. The product is our C program, which begins its life as three a source file. As it progresses through the production line, it is worked upon by four programs--the preprocessor, compiler, assembler, and linker--each of which transforms the program one step closer to a finished product. By the end, the program emerges as an executable file.&#x20;

### Saving preprocessed, compiled, and assembled versions

gcc -o hello hello.c --save-temps

This command will generate the following files in addition to the executable hello:

* hello.i: The result of the preprocessing stage.
* hello.s: The assembly code generated from the C source.
* hello.o: The object file generated from the assembly code.

### Isolating Each Stage of Compilation





### Motivation

Why are we concerning ourselves with the internals of how GCC performs compilation? After all, we regularly use programs without having any knowledge of their inner workings, focusing only on their output. Take the 'ls' command, for instance; we use it to list directory contents, but we don’t concern ourselves with its internals. So, why do we care when it comes to GCC?

Broadly speaking, there are two reasons. First, understanding these stages aids in debugging. Let’s face it, compilation isn’t always a smooth process. Quite often, something goes wrong along the way, and what you end up with is not an executable but a cryptic error message. Without a basic understanding of how compilation works, the cause of the error is likely to be elusive, making it incredibly difficult to debug your program.

Second, GCC is designed to enable separate compilation. This will be discussed in depth in the chapter on Make. In order to take advantage of separate compilation, however, you have to understand the process, particularly the linking phase.&#x20;

3\. Helps you understand what global variables are. This is mentioned in book when discussing linker

\
