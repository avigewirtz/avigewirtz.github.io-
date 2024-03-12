# The Four Stages

When you invoke GCC on a C program, it builds your program in The transformation of a C program from source code to executable involves four dist

* this section should be a bit more in depth. give specific examples. Next section will apply it



The processes of transforming C source code into executable machine code resembles an assembly line in a factory. The product is a C program, which begins it's journey as one or more source files. As it progresses down the assembly line, it gets worked on by four distinct tools--the preprocessor, compiler, assembler, and linker. At the end, the program emerges as an executable file.&#x20;

Thankfully, we don't have to invoke all four of these programs ourselves in order to build a program. gcc handles all the work for us.&#x20;



stages: preprocessing, compilation, assembly, and linking. Thankfully, we typically don't have to worry about any of this when building a program.  We simply&#x20;





Consider the multi-file C program shown below. It will serve as a running example throughout this chapter, allowing us to demonstrate how the GCC build process works.

{% tabs %}
{% tab title="testcircle.c" %}
{% code lineNumbers="true" %}
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
   
int main(void) {

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
{% endcode %}
{% endtab %}

{% tab title="circle.c" %}
{% code lineNumbers="true" %}
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
{% endcode %}
{% endtab %}

{% tab title="circle.h" %}
{% code lineNumbers="true" %}
```c
#ifndef CIRCLE_H
#define CIRCLE_H

double area(double radius);

#endif
```
{% endcode %}
{% endtab %}
{% endtabs %}

Building our program involves a lot of work. Must go through assembly line of programs.&#x20;

To build our program, we invoke the following command:

```bash
gcc217 testcircle.c circle.c -o testcircle
```

Note that the `-o` option specifies that the executable be named _testcircle_, rather than the default name a.out. To run testcircle, we simply invoke its pathname on the command line:

```
./testcircle
```

Behind the scenes, quite a lot of work is involved in producing the executable. The sequence of operations is shown in Figure 4.2. Here's a breakdown of what happens at each stage:

1. **Preprocessing stage:** The preprocessor modifies the source code in _testcircle.c_ and _circle.c_ by including header files (stdio.h, stdlib.h, and circle.h), expanding macros (such as PI), and removing comments. The output is of the preprocessor is stored in _testcircle.i_ and _circle.i_.
2. **Compilation stage:** The compiler translates _testcircle.i_ and _circle.i_ into assembly language files _testcircle.s_ and _circle.s._
3. **Assembly stage:** The assembler translates _testcircle.s_ and _circle.s_ into relocatable object files _testcircle.o_ and _circle.o_. These files contain machine code but are not executable.
4. **Linking stage:** The linker combines _testcircle.o_ and _circle.o_, along with necessary .o files from the C Standard Library, producing the executable file _testcircle_.

<figure><img src="../../.gitbook/assets/Group 63.png" alt=""><figcaption><p>Figure 4.2: GCC Four-Stage Build Process</p></figcaption></figure>

It's important to recognize that the first three stages (preprocessing, compilation, and assembly) are performed on each file separately. It is only during the linking phase that their contents are combined.

### Saving Intermediate Files

By default, gcc does not retain the intermediate files (i.e., `.i`, `.s`, and `.o)`generated during the build process. Hence, if we invoke `ls` after building testcircle, we will not see any intermediate files:

```bash
> ls
circle.h    testcircle    testcircle.c    circle.c
```

We can instruct gcc to save the intermediate files by using the `--save-temps` option:

```
gcc217 --save-temps testcircle.c circle.c -o testcircle
```

Invoking `ls`, we now see the intermediate files in our project directory:

```bash
> ls
circle.h      circle.o      testcircle    testcircle.c  testcircle.o
circle.c      circle.i      circle.s      testcircle.i  testcircle.s 
```

### Performing each stage individually

When you invoke gcc, by default it performs all stages necessary to generate an executable. For example, if you invoke gcc on a `.c` file, it will perform preprocessing, compilation, assembly, and linking. If you invoke gcc on a `.s` file, it will perform assembly and linking. You can stop the build process at any stage using the following options:

* `-E`: stop after preprocessing. By default, prints output on stdout
* `-S`: stop after compilation. By default, saves output in .s file(s)
* `-c`: stop after assembly. By default, saves output in .o file(s)

Here's an example of their usage for our testcircle program:

1. Preprocess circle.c and testcircle.c but do not compile. Store the results in circle.i and testcircle.i:

```
gcc217 -E circle.c -o circle.i
gcc217 -E testcircle.c -o testcircle.i
```

2. Compile circle.i and testcircle.i but do not assemble:

```
gcc217 -S circle.i testcircle.i
```

3. Assemble circle.s and testcircle.s but do not link:

```
gcc217 -c circle.s testcircle.s
```

4. Link circle.o and testcircle.o and store the result in testcircle:

```
gcc217 circle.o testcircle.o -o testcircle
```
