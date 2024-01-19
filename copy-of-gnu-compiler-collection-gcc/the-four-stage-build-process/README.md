# The Four Stage Build Process

The purpose of compilation is to transform C source code—a language resembling English and suitable for human understanding—into executable machine code—a numerical language designed for computer processing.

GCC performs compilation in four sequential stages: preprocessing, compilation proper, assembly, and linking. The goal of this chapter is to explain in detail why the process is broken up into four stages.&#x20;



The aim of this chapter is to provide a high-level overview of the GCC compilation process. From the user's point of view, compiling a C program is as simple as executing a single GCC command, such as `gcc myprog.c`. From GCC’s point of view, however, compilation is a complex process involving four distinct stages: preprocessing, compilation proper, assembly, and linking.&#x20;

We will illustrate the compilation process by following the journey of a C program from source code to executable. The program we will use is a simple program that calculates the area of a circle given its circumference. It consists of three files: main.c, circle.c, and circle.h. Their source code is written below.&#x20;

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

###

<figure><img src="../../.gitbook/assets/Group 9 (1).png" alt=""><figcaption></figcaption></figure>

###

###

### Motivation

Why are we concerning ourselves with the internals of how GCC performs compilation? After all, we regularly use programs without having any knowledge of their inner workings, focusing only on their output. Take the 'ls' command, for instance; we use it to list directory contents, but we don’t concern ourselves with its internals. So, why do we care when it comes to GCC?

Broadly speaking, there are two reasons. First, understanding these stages aids in debugging. Let’s face it, compilation isn’t always a smooth process. Quite often, something goes wrong along the way, and what you end up with is not an executable but a cryptic error message. Without a basic understanding of how compilation works, the cause of the error is likely to be elusive, making it incredibly difficult to debug your program.

Second, GCC is designed to enable separate compilation. This will be discussed in depth in the chapter on Make. In order to take advantage of separate compilation, however, you have to understand the process, particularly the linking phase.&#x20;

3\. Helps you understand what global variables are. This is mentioned in book when discussing linker

##

##

##

## Bird’s eye view of the GCC compilation process

The process of transforming our program into an executable resembles an assembly line. The product is our C program, which begins its life as three a source file. As it progresses through the production line, it is worked upon by different programs, each of which transforms the program one step closer to a finished product. By the end, the program emerges as an executable file.&#x20;

This ‘assembly line’ comprises four programs:

* Preprocessor&#x20;
* Compiler&#x20;
* Assembler
* Linker

<figure><img src="../../.gitbook/assets/Group 102 (1).png" alt="" width="188"><figcaption></figcaption></figure>

Thankfully, the process is automated by the gcc compiler driver.&#x20;

### Saving preprocessed, compiled, and assembled versions

gcc -o hello hello.c --save-temps

This command will generate the following files in addition to the executable hello:

* hello.i: The result of the preprocessing stage.
* hello.s: The assembly code generated from the C source.
* hello.o: The object file generated from the assembly code.

### Isolating Each Stage of Compilation



\
