# The Big Picture

Suppose we have a C program comprised of two .c files: foo.c, bar.c. To build our program, we invoke the following command:&#x20;

```bash
gcc217 foo.c bar.c -o foobar
```

Note that `-o foobar` specifies that the executable be named _foobar,_ rather than the default name _a.out_. To run _foobar_, we simply invoke its pathname on the command line:

```
./foobar
```

Behind the scenes, quite a lot of work is involved in producing the executable _foobar_. It involves four sequential stages: preprocessing, compilation, assembly, and linking. An overview of the process is shown in Figure 4.2. Here's a breakdown of what happens at each stage:

1.  **Preprocessing stage:** The preprocessor modifies the source code in foo.c and bar.c by performing two main tasks:

    1. **Removing comments.** Comments serve to help human readers understand the code, but are of no use to the compiler. Hence, they can be discarded before compilation begins.&#x20;
    2. **Handling preprocessor directives.** These are lines in the code that begin with a # (hash). Unlike tradsitional C code, they are meant to be interpreted by the preprocessor, not the compiler. Examples of preprocessor directives are #include (e.g., `#include <stdio.h>`) and #define (e.g., `#define PI 3.14159`). &#x20;

    The output is of the preprocessor is stored in _foo.i_ and _bar.i_.&#x20;
2. **Compilation stage:** The compiler translates _foo.i_ and _bar.i_ into assembly language files _testcircle.s_ and _circle.s._&#x20;
3. **Assembly stage:** The assembler translates _foo.s_ and _bar.s_ into relocatable object files _foo.o_ and _bar.o_. These files contain machine code but are not executable, since they contain external references. For example, foo.o might contain references to functions defined in bar.o or the C Standard Library.&#x20;
4. **Linking stage:** The linker combines _foo.o_ and _bar.o_, along with necessary .o files from the C Standard Library, producing the executable file _foobar_.

<figure><img src="../../.gitbook/assets/Group 70 (2).png" alt=""><figcaption></figcaption></figure>

Notice that the first three stages (preprocessing, compilation, and assembly) are performed on each file separately. Recognizing this is critical to understanding how the build process works.

### Saving Intermediate Files

By default, gcc does not retain the intermediate files (i.e., `.i`, `.s`, and `.o)`generated during the build process. Hence, if we invoke `ls` after building foobar, we'll only see one newly generated file--_foobar_:&#x20;

```bash
> ls
bar.c    foo.c    foobar
```

We can instruct gcc to save the intermediate files by using the `--save-temps` option, like so:

```bash
gcc217 --save-temps foo.c bar.c -o foobar
```

If we invoke `ls` now, we see all the intermediate files in our project directory:

```bash
> ls
bar.c    bar.i    bar.s    bar.o    foo.c    
foo.i    foo.s    foo.o    foobar   
```

### Stopping the build process at any stage

GCC provides command line options to halt the build process at any stage of the build process. Here's a breakdown of the available options:

**`-E`:**  This instructs GCC to stop the build process after the preprocessing stage. For example, if we were to invoke:

```bash
gcc217 -E foo.c bar.c
```

GCC would preprocess foo.c and bar.c and halt. By default, the preprocessed output will be printed on stdout. To save it to .i files, we can use the `.o` option or the `>` redirection operator:&#x20;

```bash
gcc217 -E foo.c -o foo.i
gcc217 -E bar.c -o bar.i
# or
gcc217 -E foo.c > foo.i
gcc217 -E bar.c > bar.i
```

**`-S`:** This instructs GCC to stop the build process after compilation. The input can be either .c (e.g., `gcc217 -S foo.c bar.c`) or .i files (e.g., `gcc217 -S foo.i bar.i`). In this case, GCC will automatically save the assembly code in .s files.

**`-c`:** This instructs GCC to stop the build process after assembly. The input can be either `.c`, `.i`, or `.o` files. GCC will automatically save the object code in `.o` files.&#x20;
