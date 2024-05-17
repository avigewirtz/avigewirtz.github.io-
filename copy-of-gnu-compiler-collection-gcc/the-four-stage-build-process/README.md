# The Big Picture

Suppose we have a C program comprised of two `.c` files: `foo.c` and `bar.c`. To build our program, we invoke the following command:

```bash
gcc217 foo.c bar.c -o foobar
```

{% hint style="info" %}
Note that `-o foobar` specifies that the executable be named `foobar`_,_ rather than the default name `a.out`.
{% endhint %}

To run `foobar`, we type its pathname on the command line:

```
./foobar
```

#### Under the Hood

Under the hood, quite a lot of work is involved in producing the executable `foobar`. It involves four sequential stages: preprocessing, compilation, assembly, and linking. An overview of the process is shown in Figure 4.2. Here's a bird's eye view of what happens at each stage:

1.  **Preprocessing stage:** The preprocessor modifies the source code in `foo.c` and `bar.c` by performing two main tasks:

    1. **Removing comments.** Comments serve to help human readers understand the code, but they are of no use to the compiler. Hence, they can be discarded before compilation begins.
    2. **Handling preprocessor directives.** These are lines in the code that begin with a `#` (hash). Unlike traditional C code, they are meant to be interpreted by the preprocessor, not the compiler. An example of a preprocessor directive is `#include` (e.g., `#include <stdio.h>`), which instructs the preprocessor to insert the contents of the specified file in the location where the `#include` directive appears.

    The output is of the preprocessor is stored in `foo.i` and `bar.i.`
2. **Compilation stage:** The compiler translates `foo.i` and `bar.i` into assembly language files foo`.s` and `bar.s`.
3. **Assembly stage:** The assembler translates `foo.s` and `bar.s` into relocatable object files `foo.o` and `bar.o`. These files contain machine code but are not executable, since they contain external references.
4. **Linking stage:** The linker combines `foo.o` and `bar.o`, along with necessary `.o` files from the C Standard Library, producing the executable object file `foobar`.

<figure><img src="../../.gitbook/assets/Frame 27 (1).png" alt=""><figcaption></figcaption></figure>

Notice that the first three stages of the build process (i.e., preprocessing, compilation, and assembly) are performed on each file separately. Recognizing this is critical to understanding how the build process works.

{% hint style="info" %}
**Insight**

* Although `gcc` (that is, lowercase `gcc`, the program we invoke on the command line) is often colloquially referred to as a compiler, it is technically a driver program, meaning it delegates the actual build tasks to other programs. These programs include `cpp` (C preprocessor), `cc1` (C compiler), `as` (assembler), and `ld` (linker). `gcc` invokes each of these programs with the necessary command line options. You can see the full sequence of operations by invoking `gcc` with the `-v` (verbose) option. You will gain a much greater appreciation of the role the `gcc` driver program plays in simplifying the build process.
* In current GCC implementations, the preprocessor (`cpp`) is integrated into the compiler (`cc1`). The underlying sequence of operations is the same, but technically the first two build steps are performed by a single program (`cc1`).
* Our build model assumes _static linking_, where all linking takes place before runtime. In practice, however, _dynamic linking_ may be used, where linking is performed during runtime.
{% endhint %}

#### Saving Intermediate Files

By default, `gcc` does not retain the intermediate files generated during the build process. Thus, if we invoke `ls` after building `foobar`, we won't see the `.i`, `.s`, or `.o` files:

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

#### Halting the Build Process at Any Stage

`gcc` provides command line options to halt the build process at any of the intermediate stages. Here's a breakdown of the options:

**`-E`:** This instructs `gcc` to halt the build process after the preprocessing stage. For example, if we invoke:

```bash
gcc217 -E foo.c bar.c
```

`gcc` will preprocess `foo.c` and `bar.c` and halt. By default, the preprocessed output will be printed on stdout. To save it to `.i` files, we can use the `.o` option or the `>` redirection operator:

```bash
gcc217 -E foo.c -o foo.i
gcc217 -E bar.c -o bar.i
# or
gcc217 -E foo.c > foo.i
gcc217 -E bar.c > bar.i
```

**`-S`:** This instructs `gcc` to halt the build process after compilation. The input can be `.c` files (e.g., `gcc217 -S foo.c bar.c`), `.i` files (e.g., `gcc217 -S foo.i bar.i`), or even a mix of both (e.g., `gcc217 -S foo.c bar.i`). `gcc` will infer which stages to perform based on the file extension--preprocessing and compilation for `.c` files, and compilation only for `.i` files. The output will automatically be saved in `.s` files.

**`-c`:** This instructs `gcc` to halt the build process after assembly. As you might expect, the input can be `.i`, `.c`, or `.s` files, and `gcc` will infer which stages to perform based on the file extension. The output will automatically be saved in `.o` files.
