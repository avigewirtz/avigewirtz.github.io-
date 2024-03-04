# 4-Stage Build Process



## The Big Picture

Consider the program in Figure 2. It will serve as a running example throughout this chapter, allowing us to provide an overview how how the build process works. Consists of three source files. circle.c, testcircle.c, and circle.h.&#x20;

{% tabs %}
{% tab title="testcircle.c" %}
```c
/*-----------------------------------------------------*/
/* testcircle.c                                        */
/*                                                     */
/* Calculates the area of a circle given its radius.   */
/*-----------------------------------------------------*/
 
#include <stdio.h>
#include <stdlib.h> 
#include "circle.h" 

/* Prompts user for radius of circle. Returns 
   EXIT_FAILURE if input is invalid. Otherwise, prints 
   circle's area to stdout and returns 0. */  
   
int main() {

  double radius, area; 

  printf("Enter radius of circle: ");
  if (scanf("%lf", &radius) != 1 || radius <= 0) {
    printf("Invalid input. Must be a positive number.\n");
    exit(EXIT_FAILURE);
  }

  area = calculateArea(radius);

  printf("The area of the circle is: %.2f\n", area);

  return 0;
}

```
{% endtab %}

{% tab title="circle.c" %}
```c
/*-----------------------------------------------------*/
/* circle.c                                            */
/*-----------------------------------------------------*/

#include "circle.h"
#define PI 3.14159

/* calculates the area of a circle given its radius */
double calculateArea(double radius) {
    return PI * radius * radius;
}
```
{% endtab %}

{% tab title="circle.h" %}
```c
#ifndef CIRCLE_H
#define CIRCLE_H

double calculateArea(double radius);

#endif
```
{% endtab %}
{% endtabs %}

To build our program, we can invoke the following command:

```bash
gcc217 testcircle.c circle.c -o testcircle
```

gcc will run the preprocessor, compiler, assembler, and linker on our program, generating the executable file _testcircle_. An overview of this process is shown in Figure 2. Here's a breakdown of what happens at each stage:

1. **Preprocessing stage:** The preprocessor modifies _testcircle.c_ and _circle.c_ by including header files (stdio.h, stdlib.h, and circle.h), expanding macros, and removing comments. Output is preprocessed source files _testcircle.i_ and _circle.i_. &#x20;
2. **Compilation stage:** The compiler translates _testcircle.i_ and _circle.i_ into assembly language files _testcircle.s_ and _circle.s._&#x20;
3. **Assembly stage:** The assembler translates _testcircle.s_ and _circle.s_ into relocatable object files _testcircle.o_ and _circle.o_. These files contain machine code but are not executable.&#x20;
4. **Linking stage:** The linker combines _testcircle.o_ and _circle.o_, along with relevant C library files, producing executable file _testcircle_.&#x20;

<figure><img src="../../.gitbook/assets/Group 63.png" alt=""><figcaption><p>Figure 2: GCC Build Process of testcircle.c and circle.c</p></figcaption></figure>

To run the _testcircle_, simply type its pathname on the command line:

```
./testcircle
```

It's important to recognize that the first three stages (preprocessing, compilation, and assembly) are performed on each file separately. This technique is known as _separate compilation_.&#x20;

## Saving Intermediate Files

By default, the intermediate files generated during the build process will not be retained. You can instruct gcc to retain the intermediate files by using the --save-temps option:

```
gcc217 --save-temps testcircle.c circle.c -o testcircle
```

Invoking ls, you will now see that all intermediate files are in your project directory:

```bash
> ls
circle.h      circle.o      testcircle    testcircle.c  testcircle.o
circle.c      circle.i      circle.s      testcircle.i  testcircle.s 
```





&#x20;

{% tabs %}
{% tab title="testcircle.c" %}
```c
...
int printf(char *format, …);
int scanf(const char *format, ...);
...

...
void exit (int status)
...

double calculateArea(double radius);

int main() {

  double radius, area;

  printf("Enter the radius of the circle: ");
  if (scanf("%lf", &radius) != 1 || circumference <= 0) { 
    printf("Invalid input. Must be a positive number.\n");
    exit(1);
  }

  area = calculateArea(radius);

  printf("The area of the circle is: %.2f\n", area);

  return 0;
}
```
{% endtab %}

{% tab title="circle.c" %}
```c
double calculateArea(double radius);

double calculateArea(double radius) {
    return 3.14159 * radius * radius;
}
```
{% endtab %}
{% endtabs %}
