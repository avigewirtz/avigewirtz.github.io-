# GCC Build Process



## The Big Picture

Consider the program in Figure 2. It will serve as a running example throughout this chapter, allowing us to provide an overview how how the build process works. Consists of three source files. circle.c, testcircle.c, and circle.h.&#x20;

{% tabs %}
{% tab title="testcircle.c" %}
```c


INCLUDE COMMENTS 

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
{% endtab %}

{% tab title="circle.c" %}
```c
#include "circle.h"
#define PI 3.14159

double calculateArea(double circumference) {
    double radius = circumference / (2 * PI);
    return PI * radius * radius;
}

```
{% endtab %}

{% tab title="circle.h" %}
```c
#ifndef CIRCLE_H
#define CIRCLE_H

double calculateArea(double circumference);

#endif
```
{% endtab %}
{% endtabs %}

To build our program, we can invoke the following command:

```bash
gcc217 testcircle.c circle.c -o testcircle
```

gcc will run the preprocessor, compiler, assembler, and linker on our program, generating the executable file _testcircle_. An overview of this process is shown in Figure 2. Here's a breakdown of what happens at each stage:

1. **Preprocessor:** Modifies testcircle.c and circle.c by including header files (stdio.h, stdlib.h, and circle.h), expanding macros, and removing comments. Output is preprocessed source files testcircle.i and circle.i. &#x20;
2. **Compiler:** Translates testcircle.i and circle.i into assembly language files testcircle.s and circle.s.&#x20;
3. **Assembler:** Translates testcircle.s and circle.s into relocatable object files testcircle.o and circle.o. These files contain machine code, but are not executable.&#x20;
4. **Linker:** Combines testcircle.o and circle.o, along with relevant C library files, into a single executable file (testcircle).&#x20;

<figure><img src="../../.gitbook/assets/Group 63.png" alt=""><figcaption></figcaption></figure>

It's important to recognize that the first three stages (preprocessing, compilation, and assembly) are performed on each file separately. This technique is known as _separate compilation_.&#x20;

To run the testcircle, simply type its pathname on the command line:

```
./testcircle
```

## Saving intermediate files

By default, the intermediate files generating during the build process will not be retained. This is why when you run gcc, you're not used to seeing all the aforementioned files in your directory. You can instruct gcc to save the intermediate files by using the --save-temps option:

```
gcc217 --save-temps testcircle.c circle.c -o testcircle
```

Invoking ls, you will now see the intermediate files in your project directory:

```
ls
```
