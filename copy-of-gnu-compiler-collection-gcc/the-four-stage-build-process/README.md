# The Big Picture: From Source Code to Executable

Consider the C program shown below. It will serve as a running example throughout this chapter, allowing us to demonstrate how the GCC build process works.&#x20;

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

double calculateArea(double radius);

#endif
```
{% endcode %}
{% endtab %}
{% endtabs %}

We can build our program by invoking the following command:

```bash
gcc217 testcircle.c circle.c -o testcircle
```

gcc will run the preprocessor, compiler, assembler, and linker on our program, generating the executable file _testcircle_. This sequence of operations is shown in Figure 4.2. Here's a breakdown of what happens at each stage:

1. **Preprocessing stage:** The preprocessor modifies _testcircle.c_ and _circle.c_ by including header files (stdio.h, stdlib.h, and circle.h), expanding macros (such as PI), and removing comments. The output is of the preprocessor is _testcircle.i_ and _circle.i_. &#x20;
2. **Compilation stage:** The compiler translates _testcircle.i_ and _circle.i_ into assembly language files _testcircle.s_ and _circle.s._&#x20;
3. **Assembly stage:** The assembler translates _testcircle.s_ and _circle.s_ into relocatable object files _testcircle.o_ and _circle.o_. These files contain machine code but are not executable.&#x20;
4. **Linking stage:** The linker combines _testcircle.o_ and _circle.o_, along with relevant C library files, producing the executable file _testcircle_.

<figure><img src="../../.gitbook/assets/Group 63.png" alt=""><figcaption><p>Figure 4.2: GCC Four-Stage Build Process </p></figcaption></figure>

_testcircle_ can be run by invoking it's pathname on the command line_:_

```
./testcircle
```

It's important to recognize that the first three stages (preprocessing, compilation, and assembly) are performed on each file separately. Thus, when, for example, the preprocessor, compiler, and assembler are processing testcircle.c, they have no knowledge of circle.c, and vice versa. It is only during the linking phase that external references are resolved.&#x20;

### Saving Intermediate Files

By default, gcc does not retain the intermediate files (`.i`, `.s`, and `.o)`generated during the build process. They are stored in temporary files, which are discarded. Hence, if you invoke `ls`, you will only see the source files and the executable:

```bash
> ls
circle.h    testcircle    testcircle.c    circle.c
```

We can instruct gcc to save the intermediate files by using the `--save-temps` option:

```
gcc217 --save-temps testcircle.c circle.c -o testcircle
```

Invoking `ls`, you will now see the intermediate files in your project directory:

```bash
> ls
circle.h      circle.o      testcircle    testcircle.c  testcircle.o
circle.c      circle.i      circle.s      testcircle.i  testcircle.s 
```

### Performing each stage individually

When you invoke gcc, by default it performs all stages necessary to generate an executable. For example, if you invoke gcc on a `.c` file, it will perform preprocessing, compilation, assembly, and linking. If you invoke gcc on a `.s` file, it will perform assembly and linking. You can stop the build process at any stage using the following options:&#x20;

* `-E`:    stop after preprocessing. By default, prints output on stdout
* `-S`:    stop after compilation. By default, saves output in .s file(s)
* `-c`:    stop after assembly. By default, saves output in .o file(s)

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

