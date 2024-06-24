# Example: Single-file Program

Now that we have a high-level understanding of the four stage build process, let's walk through it using a real program as an example. Our example program will be the `charcount` program from lecture 3, whose source code is shown below. Recall that this program counts the number of characters input through stdin and outputs the count to stdout.

{% code title="charcount.c" lineNumbers="true" %}
```c
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

Our program begins as a C source file, stored in charcount.c. We can roughly divide the source code into three categories:

* **Comments**, meant for human readers.
* **Preprocessing language**, meant for preprocessor. The preprocessing language in our program consists of the `#include <stdio.h>` directive and the `EOF` macro. More on these shortly.&#x20;
* **Raw C code** (i.e., everything else).&#x20;

Of note is that our program make calls to two library functions: `printf` and `getchar`. Their definitions will be inserted at link time.&#x20;

### Preprocessing

The first step to building our program is to preprocess it. The command to invoke the preprocessor is:

```bash
gcc217 -E charcount.c -o charcount.i
```

The result is the preprocessed file `charcount.i`. Let's break down what the preprocessor does.

1. removes the `/* Write to stdout the number of chars in stdin. Return 0. */` comment on line 3, replacing it with a space character.&#x20;
2. Next, it inserts the contents of `stdio.h`. The #include \<stdio.h> directive tells the preprocessor to grab the contents of `stdio.h` (typically located in `/usr/include`) and paste it into our program right where the `#include` directive appears. stdio.h is a large file, containing function declarations and macro definitions. Of note are the following three lines:&#x20;

```c
int printf(const char *format, ...);
int getChar(void);
#define EOF -1
```

Purpose of inserting these is to provide information to the compiler so it can type check that they're used correctly. Compiler wouldn't otherwise be able to type check, since the definitions are only inserted at link time.&#x20;

3. Expands the `EOF` macro to -1.&#x20;

You can view the preprocessed output in `charcount.i` with a text editor like emacs. You'll find that the file has expanded significantly, typically to around 500-700 lines. Most of this additional content comes from `stdio.h` .  The relevant part is shown below.&#x20;

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

Notice that the comment is removed, the contents of stdio.h were inserted, and the EOF macro was replaced with -1. At this point, our program contains raw C code only, with declarations of printf and getChar functions at the top.

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

Next, the compiler checks for semantic errors. Semantic errors occur when the syntax is correct, but you attempt to perform an illegal operation, such as using a variable before it is declared or passing a ... to a function that expects a ... It is during this stage where the purpose of inserting the declarations of `printf` and `getchar` become evident.&#x20;

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

The next step is to translate our code yet again--this time, from assembly to machine code--the sequence of 1s and 0s that the CPU "understands". Because there's typically a one-to-one correspondence between assembly-language instructions and machine-language instructions, this translation is much simpler than compilation. We run the assembler on `charcount.s` with the following command:

```c
gcc217 -c charcount.s
```


Our program is now in machine language form, stored in charcount.o. It is not executable, however, since it’s missing the definitions of the library functions printf and getChar.&#x20;

#### Linking&#x20;

