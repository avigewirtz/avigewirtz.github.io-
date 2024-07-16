# Example: charcount.c

Now that we have a high-level understanding of the four stage build process, let's walk through it in practice. Our example program will be the `charcount` program from lecture 3, whose source code is shown below. This program counts the number of characters input through stdin and outputs the count to stdout.

{% code title="charcount.c" lineNumbers="true" %}
```c
/*--------------------------------------------------------------------*/
/* testintmath.c                                                      */
/* Author: Bob Dondero                                                */
/*--------------------------------------------------------------------*/

#include <stdio.h>

/* Write to stdout the number of chars in stdin. Return 0. */
int main(void) {
    int c;
    int charCount = 0;

    c = getchar();
    while (c != EOF) {
        charCount++;
        c = getchar();
    }

    printf("%d\n", charCount);
    return 0;
}
```
{% endcode %}

#### The Starting Point

Our program begins as C source code. We can roughly divide the source code into three categories:

* **Comments**, such as `/* Write to stdout the number of chars in stdin. Return 0. */` on line 8. Comments are meant for human readers.
* **Preprocessing language. Defined by GNU as "**_directives_ to be executed and _macros_ to be expanded." The preprocessing language in our program consists of the preprocessor directive `#include <stdio.h>`  and the macro `EOF`.&#x20;
* **Raw C code** (i.e., everything else). Raw C code is meant to be translated by the compiler.

### Preprocessing

* maybe I should mention the three things it does

As we mentioned earlier, we can perform all four build steps via a single `gcc` command, or we can perform each stage individually. Here, we'll perform each stage individually.&#x20;

To run the preprocessor and halt, we use the -E option. output The command to invoke the preprocessor is:

```bash
gcc217 -E charcount.c -o charcount.i
```

Let's break down what takes place during this stage. The preprocessor is responsible for performing textual transformations on the source code before the actual compilation begins. The preprocessor doesn't understand C syntax; it operates purely on the text level.



First, the preprocessor removes all comments from the source code. Comments serve to help human readers understand the code, but they are of no use to the compiler. Hence, they can be discarded before compilation begins.&#x20;

Next, the preprocessor handles preprocessor directives. Our program contains only one explicit preprocessor directive: `#include <stdio.h>`. This instructs the preprocessor to grab the contents of `stdio.h` and paste it directly into `charcount.c` where the `#include` directive appears.

stdio.h is a large file, containing function declarations and macro definitions. For our purposes, we need only be concerned with the following three lines:

```c
...
int printf(const char *format, ...);
int getChar(void);
#define EOF -1
...
```

Purpose of inserting these is to provide information to the compiler so it can type check that they're used correctly. Compiler wouldn't otherwise be able to type check, since the definitions are only inserted at link time.

Finally, it replaces the `EOF` macro with its value, -1.

You can view the contents of `charcount.i` with a text editor like emacs. You'll find that the program has expanded to around 500-700 lines. Most of this additional content comes from `stdio.h` . For simplicity, only the relevant parts are shown below.

{% code title="charcount.i" %}
```c
...
int printf(const char *format, ...);
int getChar(void);
...

int main(void) {
    int c;
    int charCount = 0;

    c = getchar();
    while (c != -1) {
        charCount++;
        c = getchar();
    }

    printf("%d\n", charCount);
    return 0;
}
```
{% endcode %}

{% hint style="success" %}
You can think of the preprocessor as a "search-and-replace" tool:

* It replaces each comment with a whitespace character.
* It replaces each `#include` directive with the contents of the specified file.
* It replaces each macro with its value.
{% endhint %}

### Compilation

The next step is to run the compiler on `charcount.i`. We do so with the following command:

```bash
gcc217 -S charcount.i
```

The output is assembly language file `charcount.s`. Let's break down what takes place during this stage.

#### Error Checking

First, the compiler checks for syntax errors in our code. Syntax errors occur if you don’t follow the grammar rules of the C language. For example, forgetting a semicolon or a curly brace. Thankfully we don’t have any syntax errors, but if we did, the compiler would report the errors and terminate.

Next, the compiler checks for semantic errors. Semantic errors occur when the syntax is correct, but you attempt to perform an illegal operation, such as using a variable before it is declared or passing a ... to a function that expects a ... It is during this stage where the purpose of inserting the declarations of `printf` and `getchar` become evident.

#### Translation to Assembly

Given that our code does not contain any syntax or semantics errors, the compiler then moves on to translating it to the assembly language of the target architecture. On an ARM64 machine, the assembly will look something like this:

{% code title="charcount.s" %}
```armasm
.LC0:
        .string "%d\n"
main:
        stp     x29, x30, [sp, -32]!
        mov     x29, sp
        str     wzr, [sp, 24]
        bl      getchar
        str     w0, [sp, 28]
        b       .L2
.L3:
        ldr     w0, [sp, 24]
        add     w0, w0, 1
        str     w0, [sp, 24]
        bl      getchar
        str     w0, [sp, 28]
.L2:
        ldr     w0, [sp, 28]
        cmn     w0, #1
        bne     .L3
        ldr     w1, [sp, 24]
        adrp    x0, .LC0
        add     x0, x0, :lo12:.LC0
        bl      printf
        mov     w0, 0
        ldp     x29, x30, [sp], 32
        ret
```
{% endcode %}

You don't need to understand what any of this means. ARM64 assembly will be covered in detail in the second half of COS217. For now, a few points are worth noting.

*   Each assembly instruction performs a very basic task, such as adding two numbers or moving data from one memory location to another. As such, it has a poor ratio of functionality to code size compared to higher-level languages like C. In our example, the simple statement getChar++ maps to four ARM assembly instructions:

    ```armasm
    LDR     w0, [sp, 24]
    ADD     w0, w0, 1
    STR     w0, [sp, 24]
    ```
* Assembly language gives you total control over the CPU. Some operations possible in assembly have no high-level language equivalent. This allows you to optimize performance and resource usage to a degree not possible in higher-level languages.
* One of the main drawbacks of assembly is that it's not portable. Unlike high-level languages like C, \<fill in>.

#### Assembly

The next step is to translate our code yet again--this time, from assembly to machine code. Machine code is a binary language, consisting of 1s and 0s. Because there's typically a one-to-one correspondence between assembly-language instructions and machine-language instructions, this translation is much simpler than compilation. We run the assembler on `charcount.s` with the following command:

```c
gcc217 -c charcount.s
```

Our program is now in machine language form, stored in charcount.o. It is not executable, however, since it’s missing the definitions of the library functions printf and getChar.

#### Linking

The final stage in the build process is the linking stage. Here, the linker inserts the definitions of the printf and getChar library functions into our program, making it a complete, executable program.

We invoke the linker with the following command:

gcc charcount.o -o charcount

The output is charcount, which can be loaded into memory and run.

A couple of points about the linking stage are worth noting.

1. The C library is stored in libc.a.
2. The linker extracts only the relevant code from libc.a.
3. Typically, the name of libraries we’re linking against must be supplied as an argument in the linking command. However, we’d need not supply libc.a, since GCC automatically supplied it to linker.
