# Example

Let's now analyze each of the build stages in practice. As an example, we'll use the multi-file C program shown below. The program consists of three files:  `testcircle.c`, `circle.c`, and `circle.h`. `testcircle.c` contains the `main` function, the entry point of our program. It prompts the user for the radius of a circle and prints its area on stdout. `circle.c` contains the implementation of `calculateArea`, the function that calculates the circle's area. Finally, `circle.h` contains the declaration of `calculateArea`.

{% tabs %}
{% tab title="testcircle.c (client)" %}
```c
/*--------------------------------------------------------------------*/
/* testcircle.c                                                       */
/*                                                                    */
/* Calculates the area of a circle given its radius.                  */
/*--------------------------------------------------------------------*/
 
#include <stdio.h>
#include <stdlib.h>
#include "circle.h"

/* Prompts user for the radius of a circle. Returns
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
{% endtab %}

{% tab title="circle.c (implementation)" %}
```c
/*--------------------------------------------------------------------*/
/* circle.c                                                           */
/*--------------------------------------------------------------------*/

#include "circle.h"
#define PI 3.14159

double calculateArea(double radius) {
    return PI * radius * radius;
}
```
{% endtab %}

{% tab title="circle.h (interface)" %}
```c
#ifndef CIRCLE_H
#define CIRCLE_H

double calculateArea(double radius);

#endif
```
{% endtab %}
{% endtabs %}

### The Starting Point

At this point, our program is currently in the following state:

* C language. Can roughly divide into three categories:
  * Raw C (for compiler)
  * Preprocessing language (for preprocessor)
  * Comments (for humans)

testcircle.c is missing both the definitions and the declarations are four functions: printf, scanf, exit, and calculateArea. Additionally, it uses the preprocessor macro EXIT\_FAILURE, but there's no indication of what it is.&#x20;

{% hint style="info" %}
**Declaration vs. definition**


{% endhint %}

### Preprocessing Stage

The build process begins with preprocessing. We can invoke the preprocessor alone with the following commands:

```bash
gcc217 -E tescircle.c > testcircle.i
gcc217 -E circle.c > circle.i
```

The result is two preprocessed files: `testcircle.i`, and `circle.i`. As we mentioned earlier, the preprocessor performs two main tasks: It removes comments, which are of no use to the compiler, and handles preprocessor directives (lines in the code that begin with a `#`). Let's now break down how the preprocessor transoforms testcircle.c and circle.c respectievly.&#x20;

Our program makes use of three types of preprocessor directives: `#include`, `#define`, and `#ifndef`/ `#endif`. These directives control file inclusion, macro definition, and conditional compilation respectively.&#x20;

#### File Inclusion

The `#include` directive instructs the preprocessor to grab the contents of the specified file and paste it directly into the current file where the `#include` directive appears. In testcircle.c, the preprocessor inserts the contents This means that the preprocessor will paste `circle.h` right where #include "circle.h" appears in  both `circle.c` and `testcircle.c`, and `stdio.h` and `stdlib.h` in `testcircle.c`

The preprocessor pastes the contents of `stdio.h`, `stdlib.h`, and `circle.h` right where these directives appear. `stdio.h` and `stdlib.h` are C library header files. `stdio.h` contains declarations of Standard I/O functions, such as `printf` and `scanf` , while `stdlib.h` contains declarations of general utility functions, such as `exit`. circle.h, of course, contains the declaration of calculateArea.

Inserting these declarations enables the compiler to ensure that the types of the arguments and return value match up correctly between the function call and the function definition.









&#x20;Including these declarations enables the compiler to ensure that the argument types and return value match up correctly between the function call and the function definition.&#x20;

, which contain the For example, in `testcircle.c`, the preprocessor replaces `#include <stdio.h>` with the contents of `stdio.h`. #included files are typically header files, which contain the declarations of externally defined functions.&#x20;

The purpose of #including header files is to&#x20;

{% hint style="info" %}
Notice that there are two syntaxes for the `#include` directive: with angle brackets (e.g., `#include <stdio.h>`), and with double quotes (e.g., `#include "circle.h"`). The difference between these two syntaxes lies in how the preprocessor searches for the specified file, with the precise details being implementation-defined. In general, files included with angle brackets are searched for in system directories only, while those included with double quotes are searched for in the working directory first and then in system directories.
{% endhint %}

#### Macro Definition

The `#define` directive creates a preprocessor macro, which is essentially an alias for a specific value or code snippet. In `circle.c`, `#define PI 3.14159` creates the macro `PI` and assigns it the value `3.14159`. Whenever `PI` is subsequently used in `circle.c`, the preprocessor replaces it with `3.14159`.

#### Conditional Compilation

The `#ifndef` / `#else` directives, which we use in `intmath.h`, are part of a set of directives known as _conditional_ directives. These are used to control which parts of the source code are sent to the compiler. One of their most common use cases is to prevent the contents of a header file from being included twice in the same compilation unit (i.e., `.i` file). This technique is known as an _#include guard_. Here's how it works in `intmath.h`:

* `#ifndef CIRCLE_H`: This checks if the macro `CIRCLE_H` is defined. If this evaluates to TRUE (i.e., `CIRCLE_H` is not defined), the preprocessor continues to process the code between `#ifndef` and `#endif`. If it evaluates to FALSE, the preprocessor skips the entire block within `#ifndef` ... `#endif`.
* `#define CIRCLE_H`: This defines `CIRCLE_H`. Notice that it doesn't give `CIRCLE_H` any specific value. This is perfectly valid. The preprocessor will simply note that `CIRCLE_H` is defined.
* `#endif`: This line ends the conditional block started by `#ifndef`.

{% hint style="success" %}
You can think of the preprocessor as a "search-and-replace" tool:

* It replaces each comment with a whitespace character.
* It replaces each `#include` directive with the contents of the specified file.
* It replaces each macro with its value.
{% endhint %}

#### Examining `testcircle.i` and `circle.i`

You can view the preprocessed files with a text editor like emacs. Let’s examine `testcircle.i` and `circle.i` to see what precisely was done by the preprocessor. A side-by-side comparison is shown in Figure 12.

<figure><img src="../.gitbook/assets/Frame 61.png" alt=""><figcaption></figcaption></figure>

First, we see that the preprocessor removed all comments from `testcircle.c` and `circle.c`. Second, it replaced each `#include` directive with the contents of its specified header: `circle.h` for both `circle.c` and `testcircle.c`, and `stdio.h` and `stdlib.h` for `testcircle.c`. `stdio.h` contains declarations for the `printf` and `scanf` functions, while `stdlib.h` contains the declaration of the `exit` function and the definition of the `EXIT_FAILURE` macro. Finally, all macros were expanded: `PI` in `circle.c` was replaced with `3.14159`, and `EXIT_FAILURE` was replaced with `1`.

At this point,&#x20;

### Compilation Stage

The next stage of the build process is compilation, which is where the bulk of the work takes place. In this stage, the compiler translates `circle.i` and `testcircle.i` into assembly language files `circle.s` and `testcircle.s` (Figure 14). The compiler checks for syntax errors and type mismatches. Assembly language is essentially a human-readable version of the target processor's machine language. As such, the precise assembly language generated by the compiler will vary depending on what processor it's being generated for. For example, if the code is being compiled on a ARM64 machine, the assembly will be... If the code is being compiled on an Intel x86. it might be translated into X86-64 assembly. In figure 14, the assembly is in ARM.

<figure><img src="../.gitbook/assets/Frame 63.png" alt="" width="563"><figcaption></figcaption></figure>

#### Characteristics Assembly language

Detailed coverage of assembly or machine language is beyond the scope of this chapter. ARM64 assembly will be covered in detail in the second half of the course. For now, we will make a few general points about assembly.

* Not portable. Portability refers to how easy it is to translate a language into the machine language for any arbitrary processor. Portable languages such as C can be translated into the machine into This means that an assembly program written in one language, such as ARM**Assembly is basically** a human-readable version of the target processor's machine language. There is typically a one-to-one mapping between an assembly language instruction and a machine language instruction. For example, the ARM assembly instruction `ADD X0, X1, X2` translates directly into a machine code instruction that adds the values in registers X1 and X2 and stores the result in register X0.
*   Extremely simple. Each instruction does a simple task, such as adding two numbers or moving data from one memory location to another. A single C statement might take several instructions. For example, a simple like statement like `x = y + z` might require four ARM assembly instructions:

    ```armasm
    LDR X0, [y]      // Load the value of y into register X0 
    LDR X1, [z]      // Load the value of z into register X1
    ADD X0, X0, X1   // Add the values in X0 and X1, store result in X0
    STR X0, [x]      // Store the result from X0 into the variable x
    ```
* Programmers rarely program in assembly, since modern compilers can produce code as good as humans. However, still has its place in modern computing. Gives you more direct control over hardare. Some instructions cannot be performed in C. Assembly language might be used to optimize performance-critical sections of code, to write low-level device drivers, or to develop code for embedded systems with limited resources.

### Assembly Stage

When an assembler generates an object module, it does not know where the code and data will ultimately be stored in memory. Nor does it know the locations of any externally defined functions or global variables that are referenced by the module. So whenever the assembler encounters a reference to an object whose ultimate location is unknown, it generates a relocation entry that tells the linker how to modify the reference when it merges the object file into an executable.

The purpose of the assembler is to convert assembly language into machine code and generate an object file. When there are calls to external functions in the assembly source file, the assembler leaves the addresses of the external functions undefined, to be filled in later by the linker

The next stage of the build process is assembly. In this stage, `circle.s` and `testcircle.s` are sent to the assembler, which translates them into relocatable object files `circle.o` and `testcircle.o` (Figure 15). These relocatable object files are essentially machine-code equivalents of `circle.s` and `testcircle.s` (and, by extension, of `circle.i` and `testcircle.i`). However, they also contain metadata for the linker.

<figure><img src="../.gitbook/assets/Frame 62.png" alt="" width="563"><figcaption></figcaption></figure>

Contains binary code and data in a form that can be combined with other relocatable object files at compile time to create an executable object file.

Object files are merely collections of blocks of bytes. Some of these blocks contain program code, others contain program data, and others contain data structures that guide the linker and loader.

### Linking Stage

Static linkers such as the Linux LD program take as input a collection of relocatable object files and command-line arguments and generate as output a fully linked executable object file that can be loaded and run. The input relocatable object files consist of various code and data sections, where each section is a contiguous sequence of bytes. Instructions are in one section, initialized global variables are in another section, and uninitialized variables are in yet another section.

Step 1. Symbol resolution. Object files define and reference symbols, where each symbol corresponds to a function, a global variable, or a static variable (i.e., any C variable declared with the static attribute). The purpose of symbol resolution is

to associate each symbol reference with exactly one symbol definition.\
Step 2. Relocation. Compilers and assemblers generate code and data sections that start at address 0. The linker relocates these sections by associating a memory location with each symbol definition, and then modifying all of the references to those symbols so that they point to this memory location. The linker blindly performs these relocations using detailed instructions, generated by the assembler, called relocation entries.



Executable object file. Contains binary code and data in a form that can be copied directly into memory and executed.

At this point, we have two object files--circle.o and testcircle.o. These files both contain machine code, but they are not executable. circle.o has an undefined reference to \`main'. And testcircle.o has undefined references to four functions: calculateArea, exit, printf, and scanf.

In the final stage, tescircle.o and circle.o get sent to the linker. The linker combines all these files--testcircle.o, circle.o, and C library--together, resolving all external references in our program. The output is a single file--the executable testcircle. This process is shown in Figure 6.



<figure><img src="../.gitbook/assets/Frame 60 (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Understanding the role of the linker


{% endhint %}

{% hint style="info" %}
should mention starter code role of linker as aside. entry symbol \_start
{% endhint %}
