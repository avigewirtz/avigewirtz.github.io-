# The Big Picture

#### Building a Single-file C Program

Suppose we have a C program contained in a single `.c` file, `foo.c`. To build our program, we use the following command:

```bash
gcc217 foo.c -o foo
```

{% hint style="info" %}
Note that `-o foo` specifies that the executable be named `foo`_,_ rather than the default name `a.out`.
{% endhint %}

To run `foo`, we type its name on the command line, prefixed by a `./`:

```bash
./foo
```

The shell loads `foo` into memory and execute it.&#x20;

#### Under the Hood

Behind the scenes, quite a lot of work is involved in producing the executable `foo`. It involves four sequential stages: preprocessing, compilation, assembly, and linking. An overview of this process is shown in Figure 4.2. Here's a bird's eye view of what happens at each stage:

1.  **Preprocessing stage:** The preprocessor modifies the source code in `foo.c` by performing two key tasks:

    * **Removing comments.** Comments serve to help human readers understand the code, but they are of no use to the compiler. Hence, they can be discarded before compilation begins.
    * **Handling preprocessor directives.** These are lines in the code that begin with a `#` (hash). Unlike traditional C code, they are meant to be interpreted by the preprocessor, not the compiler. An example of a preprocessor directive is `#include` (e.g., `#include <stdio.h>`), which instructs the preprocessor to grab the contents of the specified file and paste it directly into the current file where the `#include` directive appears.

    The output is of the preprocessor is stored in `foo.i`.
2. **Compilation stage:** The compiler translates `foo.i`  into assembly language file `foo.s`.
3. **Assembly stage:** The assembler translates `foo.s` into _relocatable object file_ `foo.o`. This file is essentially machine code equivalent of `foo.s`. &#x20;
4. **Linking stage:** The linker combines `foo.o` with the necessary `.o` files from the C Standard Library, producing the _executable object file_ `foo`, which can be loaded into memory and executed.

<figure><img src="../../.gitbook/assets/Frame 27 (4).png" alt=""><figcaption></figcaption></figure>

The critical point to recognize is that definitions of library functions are only inserted after&#x20;

{% hint style="info" %}
**Insight**

* Although `gcc` (that is, lowercase `gcc`, the program we invoke on the command line) is often colloquially referred to as a compiler, it is technically a driver program, meaning it delegates the actual build tasks to other programs. These programs include `cpp` (C preprocessor), `cc1` (C compiler), `as` (assembler), and `ld` (linker). `gcc` invokes each of these programs with the necessary command line arguments. You can see the full sequence of operations by invoking `gcc` with the `-v` (verbose) option. You will gain a much greater appreciation of the role the `gcc` driver program plays in simplifying the build process.
* In current GCC implementations, the preprocessor (`cpp`) is integrated into the compiler (`cc1`). The underlying sequence of operations is the same, but technically the first two build steps are performed by a single program (`cc1`).
* Our build model assumes _static linking_, where all linking takes place before runtime. In practice, however, _dynamic linking_ might be used, where linking is performed during execution of the program.
{% endhint %}

#### Building a Multi-file C Program

As we know, the source code of a C program may be distributed across any arbitrary number of files.   Suppose we modify our program by dividing it into two `.c` files, `foo.c`, and `bar.c`. We build our program by supplying both files as arguments to `gcc217`:&#x20;

```bash
gcc217 foo.c bar.c -o foobar
```

The sequence of operations performed by `gcc` is summarized in Figure 12. The critical point to recognize is that the first three stages of the build process (i.e., preprocessing, compilation, and assembly) are performed on each file separately. In other words, when the preprocessor, compiler, and assembler process `foo.*`, they have no knowledge of `bar.*`, and vice versa.  This means that even if a function called&#x20;

<figure><img src="../../.gitbook/assets/Frame 27 (3).png" alt=""><figcaption></figcaption></figure>

#### Saving Intermediate Files

By default, `gcc` does not retain the intermediate files generated during the build process. Thus, if we invoke `ls` after building `foobar`, for example, we won't see any of the `.i`, `.s`, or `.o` files in our directory:

```bash
$ ls
bar.c    foo.c    foobar
```

We can instruct `gcc` to save the intermediate files by using the `--save-temps` option, like so:

```bash
gcc217 --save-temps foo.c bar.c -o foobar
```

If we invoke `ls` again, we'll now see all the intermediate files:

```bash
$ ls
bar.c    bar.i    bar.s    bar.o    foo.c    
foo.i    foo.s    foo.o    foobar   
```

#### Halting the Build Process at Any Intermediate Stage

`gcc` provides command line options to halt the build process at any of the intermediate stages. Here's a breakdown of the options:

**`-E`:** This instructs `gcc` to halt the build process after the preprocessing stage. For example, if we invoke:

```bash
gcc217 -E foo.c bar.c
```

`gcc` will preprocess `foo.c` and `bar.c` and halt. By default, the preprocessed output will be printed on stdout. To save the output in `.i` files, we can use the `.o` option or the `>` redirection operator:

```bash
gcc217 -E foo.c -o foo.i
gcc217 -E bar.c -o bar.i
# or
gcc217 -E foo.c > foo.i
gcc217 -E bar.c > bar.i
```

**`-S`:** This instructs `gcc` to halt the build process after compilation. The input can be `.c` files (e.g., `gcc217 -S foo.c bar.c`), `.i` files (e.g., `gcc217 -S foo.i bar.i`), or even a mix of both (e.g., `gcc217 -S foo.c bar.i`). `gcc` will infer which stages to perform based on the file extension--preprocessing and compilation for `.c` files, and compilation only for `.i` files. The output will automatically be saved in `.s` files.

**`-c`:** This instructs `gcc` to halt the build process after assembly. As you might expect, the input can be `.i`, `.c`, or `.s` files, and `gcc` will infer which stages to perform based on the file extension. The output will automatically be saved in `.o` files.
