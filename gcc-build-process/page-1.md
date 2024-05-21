# Example

Let's now analyze each of the build stages in practice. As an example, we'll use the multi-file C program shown below. The program consists of three files: `testcircle.c`, `circle.c`, and `circle.h`. `testcircle.c` contains the `main` function, the entry point of our program. It prompts the user for the radius of a circle, calls the calculateArea function, and prints its area on stdout. `circle.c` and `circle.h` contain the definition (i.e., implementation) and declaration of calculateArea, respectively.

{% tabs %}
{% tab title="testcircle.c (client)" %}
{% code lineNumbers="true" %}
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
{% endcode %}
{% endtab %}

{% tab title="circle.c (implementation)" %}
{% code lineNumbers="true" %}
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
{% endcode %}
{% endtab %}

{% tab title="circle.h (interface)" %}
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

### The Starting Point

Our program is currently in the following state:

* C source code. Can roughly divide it into three categories of source code:
  * Comments (for humans)
  * Preprocessor directives (for preprocessor)
  * Raw C code (for compiler)



### Preprocessing Stage

The build process begins with preprocessing. We can invoke the preprocessor on `testcircle.c` and `circle.c` with the following commands:

```bash
gcc217 -E tescircle.c > testcircle.i
gcc217 -E circle.c > circle.i
```

The result is two preprocessed files: `testcircle.i`, and `circle.i`. As we mentioned earlier, the preprocessor performs two main tasks: It removes comments, which are of no use to the compiler, and handles preprocessor directives (lines in the code that begin with a `#`). Our program makes use of three types of preprocessor directives: `#include`, `#define`, and `#ifndef`/ `#endif`. These directives control file inclusion, macro definition, and conditional compilation respectively.

#### File Inclusion

The `#include` directive instructs the preprocessor to grab the contents of the specified file and paste it directly into the current file where the `#include` directive appears. For example, in `testcircle.c`, the preprocessor replaces `#include <stdio.h>` with the contents of `stdio.h`.

{% hint style="info" %}
Notice that there are two syntaxes for the `#include` directive: with angle brackets (e.g., `#include <stdio.h>`), and with double quotes (e.g., `#include "circle.h"`). The difference between these two syntaxes lies in how the preprocessor searches for the specified file, with the precise details being implementation-defined. In general, files included with angle brackets are searched for in system directories only, while those included with double quotes are searched for in the working directory first and then in system directories.
{% endhint %}

The main use case of the `#include` directive is to insert header files, which contain, among other things, declarations of external functions. `testcircle.c` includes `stdio.h`, `stdlib.h`, and `circle.h`, which contain declarations of `printf/scanf`, `exit`, and `calculateArea`, respectively. Including these declarations in our file enables the compiler to ensure that the functions are used correctly (i.e., the argument and return types match up between the function calls and definitions).

{% hint style="info" %}
**Why is `circle.h` #included in `circle.c`?**

Although technically not necessary, including `circle.h` in `circle.c` ensures that the declaration of `calculateArea` in `circle.h` matches the definition in `circle.c`. If there's a discrepancy between the two, this will cause a compilation error, letting us know that there's a bug in our program.
{% endhint %}

#### Macro Definition

The `#define` directive creates a preprocessor macro, which is essentially an alias for a specific value or code snippet. In `circle.c`, `#define PI 3.14159` creates the macro `PI` and assigns it the value `3.14159`. Whenever `PI` is subsequently used in `circle.c`, the preprocessor replaces it with `3.14159`.

`testcircle.c` uses the preprocessr macro `EXIT_FAILURE`, which we did not define. This preprocessor directive is defined in `stdlib.h` (which we `#included` in `testcircle.c`). It's precise value is implementation-defined, but it usually equals 1--as it does in our case.&#x20;

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

First, we see that the preprocessor removed all comments from `testcircle.c` and `circle.c`. Second, it replaced each `#include` directive with the contents of its specified header: `circle.h` for both `circle.c` and `testcircle.c`, and `stdio.h` and `stdlib.h` for `testcircle.c`. `stdio.h` contains declarations for the `printf` and `scanf` functions, while `stdlib.h` contains the declaration for the `exit` function and the definition of the `EXIT_FAILURE` macro. Finally, all macros were expanded: `PI` in `circle.c` was replaced with `3.14159`, and `EXIT_FAILURE` was replaced with `1`.

### Compilation Stage

The next stage of the build process is compilation, which is where the bulk of the work takes place. The job of the compiler is to translate the preprocessed source code into assembly language. If there are any syntax errors in the C code, the compiler will report an error and terminate. We compile `testcircle.i` and `circle.i` with following command:

```
gcc217 -S testcircle.i circle.i
```

The output is assembly language files `circle.s` and `testcircle.s` . Assembly language is essentially a human-readable version of the target processor's machine language. As such, the precise assembly language generated by the compiler will vary depending on what processor it's being generated for. Figure 14 shows the assembly output for an ARM64 machine.&#x20;

<figure><img src="../.gitbook/assets/Frame 63.png" alt="" width="563"><figcaption></figcaption></figure>

#### Characteristics of Assembly language

Detailed coverage of assembly language is beyond the scope of this chapter. ARM64 assembly will be covered in detail in the second half of the course. For now, we will make a few general points about assembly. Note that these points follow from the fact assembly is&#x20;

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

The purpose of the assembler is to convert assembly language into machine code and generate a relocatable object file. When there are calls to external functions in the assembly source file, the assembler leaves the addresses of the external functions undefined, to be filled in later by the linker. When the compiler encounters a symbol (either a variable or function name) that is not defined in the current module, it assumes that it is defined in some other module, generates a linker symbol table entry, and leaves it for the linker to handle.

Object files are merely collections of blocks of bytes. Some of these blocks contain program code, others contain program data, and others contain data structures that guide the linker.&#x20;

{% hint style="info" %}
**Object File Formats**

Object files are organized according to specific object file formats, which vary from system to system. The first Unix systems from Bell Labs used the a.out format. (To this day, executables are still

referred to as a.out files.) Windows uses the Portable Executable (PE) format. Mac OS-X uses the Mach-O format. Modern x86-64

Linux and Unix systems use Executable and Linkable Format (ELF).
{% endhint %}

<figure><img src="../.gitbook/assets/Frame 62.png" alt="" width="563"><figcaption></figcaption></figure>

### Linking Stage

The final stage of the build process is linking. The linker take as input a collection of relocatable object files and generate as output a fully linked executable object file that can be loaded and run.&#x20;

The two main tasks of linkers are symbol resolution, where each global symbol in an object file is bound to a unique definition, and relocation, where the ultimate memory address for each symbol is determined and where references to those objects are modified. If the linker is unable to find a definition for the referenced symbol in any of its input modules, it prints an error message and terminates.  Multiple object files can define the same symbol, and the rules that linkers use for silently resolving these multiple definitions can introduce subtle bugs in user programs.

{% hint style="info" %}
should mention starter code role of linker as aside. entry symbol \_start
{% endhint %}

<figure><img src="../.gitbook/assets/Frame 60 (1).png" alt=""><figcaption></figcaption></figure>
