# The Big Picture

Suppose we have a C program comprised of two `.c` files: `foo.c` and `bar.c`. To build our program, we invoke the following command:&#x20;

```bash
gcc217 foo.c bar.c -o foobar
```

Note that `-o foobar` specifies that the executable be named `foobar`_,_ rather than the default name `a.out`. To run `foobar`, we type its pathname on the command line:

```
./foobar
```

Behind the scenes, quite a lot of work is involved in producing the executable `foobar`. It involves four sequential stages: preprocessing, compilation, assembly, and linking. An overview of the process is shown in Figure 4.2. Here's a bird's eye view of what happens at each stage:

1.  **Preprocessing stage:** The preprocessor modifies the source code in `foo.c` and `bar.c` by performing two main tasks:

    1. **Removing comments.** Comments serve to help human readers understand the code, but they are of no use to the compiler. Hence, they can be discarded before compilation begins.&#x20;
    2. **Handling preprocessor directives.** These are lines in the code that begin with a `#` (hash). Unlike traditional C code, they are meant to be interpreted by the preprocessor, not the compiler. An example of a preprocessor directive is `#include` (e.g., `#include <stdio.h>`), which instructs the preprocessor to insert the contents of the specified file in the location where the `#include` directive appears.&#x20;

    The output is of the preprocessor is stored in `foo.i` and `bar.i.`&#x20;
2. **Compilation stage:** The compiler translates `foo.i` and `bar.i` into assembly language files foo`.s` and `bar.s`.&#x20;
3. **Assembly stage:** The assembler translates `foo.s` and `bar.s` into relocatable object files `foo.o` and `bar.o`. These files contain machine code but are not executable, since they contain external references.&#x20;
4. **Linking stage:** The linker combines `foo.o` and `bar.o`, along with necessary `.o` files from the C Standard Library, producing the executable file `foobar`.

<figure><img src="../../.gitbook/assets/Group 70 (2).png" alt=""><figcaption></figcaption></figure>

Notice that the first three stages of the build process (preprocessing, compilation, and assembly) are performed on each file separately. Recognizing this is critical to understanding how the build process works.

{% hint style="info" %}
**Insight**

* Although `gcc` (that is, lowercase `gcc`, the program we invoke on the command line)  is often colloquially referred to as a compiler, it is technically a driver program, meaning it delegates the actual build tasks to other programs. These programs include `cpp` (C preprocessor), `cc1` (C compiler), `as` (assembler), and `ld` (linker). You can see the full sequence of commands `gcc` invokes these programs with by using the `-v` (verbose) option.
* In current GCC implementations, the preprocessor (`cpp`) is integrated into the compiler (`cc1`). The underlying sequence of operations is the same, but technically the first two build steps are performed by a single program.&#x20;
{% endhint %}

### Saving Intermediate Files

By default, gcc does not retain the intermediate files (i.e., `.i`, `.s`, and `.o)`generated during the build process. Thus, if we invoke `ls` after building `foobar`, we won't see any of the intermediate files:&#x20;

```bash
$ ls
bar.c    foo.c    foobar
```

We can instruct gcc to save the intermediate files by using the `--save-temps` option, like so:

```bash
gcc217 --save-temps foo.c bar.c -o foobar
```

If we invoke `ls` again, we'll see all the intermediate files:&#x20;

```bash
$ ls
bar.c    bar.i    bar.s    bar.o    foo.c    
foo.i    foo.s    foo.o    foobar   
```

### Stopping the build process at any stage

GCC provides command line options to halt the build process at any stage of the build process. Here's a breakdown of the available options:

**`-E`:**  This instructs GCC to stop the build process after the preprocessing stage. For example, if we were to invoke:

```bash
gcc217 -E foo.c bar.c
```

GCC would preprocess `foo.c` and `bar.c` and halt. By default, the preprocessed output will be printed on stdout. To save it to `.i` files, we can use the `.o` option or the `>` redirection operator:&#x20;

```bash
gcc217 -E foo.c -o foo.i
gcc217 -E bar.c -o bar.i
# or
gcc217 -E foo.c > foo.i
gcc217 -E bar.c > bar.i
```

**`-S`:** This instructs GCC to stop the build process after compilation. The input can be either `.c` files:&#x20;

```
gcc217 -S foo.c bar.c 
```

or `.i` files:

```
gcc217 -S foo.i bar.i
```

In the former case, GCC will preprocess and compile the files and halt. in the latter case, GCC will begin will begin with compilation and halt. GCC automatically saves the resulting assembly code in `.s` files.

**`-c`:** This instructs GCC to stop the build process after assembly. The input can be either `.c`, `.i`, or `.o` files. gcc will determine which stages to perform based on which type of file it is. For example, if the file is a .c file, gcc will begin with assembly and halt. GCC automatically saves the resulting object code in `.o` files.&#x20;
