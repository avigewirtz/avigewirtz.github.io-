# The Big Picture

Suppose we have a C program contained within a single `.c` file, `foo.c`. To build our program with `gcc`, we run the following command:

```bash
gcc217 foo.c -o foo
```

{% hint style="info" %}
Note that `-o foo` tells `gcc` to name the executable `foo`_,_ rather than the default name `a.out`.
{% endhint %}

To run `foo`, we type its name on the command line, prefixed by a `./`:

```bash
./foo
```

#### Under the Hood

As we mentioned earlier, the underlying process of transforming `foo.c` into the executable `foo` takes pace in a sequence of four stages: preprocessing, compilation, assembly, and linking. Interestingly, none of these stages is performed by the `gcc` itself (that is, the `gcc` binary, typically stored in `usr/bin`). The programs that perform the work--collectively forming a toolchain--are `cpp` (C preprocessor), `cc1` (C compiler), `as` (assembler), and `ld` (linker). `gcc` is a driver program that serves as our interface to this toolchain. It parses our command line, figures out what we want to do, and then calls these programs to do the actual work. Here's a bird's eye view of what happens during each stage:

1. **Preprocessing.** First, `gcc` sends `foo.c` to the preprocessor (`cpp`). The preprocessor performs basic modifications to the source code, such as removing comments, inserting header files, and expanding macros. Note that the latter two operations are triggered by preprocessor directives--`#include` and `#define`, respectively. More on these directives in the next section. The output of the preprocessor is `foo.i`.
2. **Compilation.** Next, `gcc` sends `foo.i` to the compiler (`cc1`). The compiler translates `foo.i` into assembly language and stores the result in `foo.s`. Assembly language is a low-level representation of the program that is close to machine code but still human-readable.
3. **Assembly.** `gcc` then send `foo.s` to the assembler (`as`), yet another translator. The assembler translates `foo.s` into machine code and stores the result in the object file `foo.o`. This is a binary file containing machine code and metadata. This file is not yet executable because it may have unresolved references to external symbols (functions and variables defined in other files or libraries).
4. **Linking.** Finally, `gcc` sends `foo.o` to the linker (`ld`). The linker combines `foo.o` with necessary object files from the C standard library. The output is the executable file `foo`.

This process is summarized in Figure 4.

<figure><img src="../.gitbook/assets/Frame 27 (5).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
A useful analogy is to think of this four stage process as an assembly line, where the product is a C program, the tools that work on the product are `cpp`, `cc1`, `as`, and `ld`, and the manager orchestrating the process is `gcc`.
{% endhint %}

{% hint style="info" %}
**Note**

* In current GCC implementations, the preprocessor (`cpp`) is integrated into the compiler (`cc1`). The underlying sequence of operations is the same, but technically the first two build steps are performed by a single program (`cc1`).
* The build model we described assumes _static linking_, where all linking takes place before the file is executed. In practice, however, _dynamic linking_ might be used, where linking is performed at runtime.
{% endhint %}

#### Saving Intermediate Files

By default, `gcc` does not retain the intermediate files generated during the build process. Thus, if we invoke `ls` after building `foo`, we won't see any of the `.i`, `.s`, or `.o` files in our directory:

```bash
$ ls
foo.c foo
```

We can instruct `gcc` to save the intermediate files by using the `--save-temps` option, like so:

```bash
gcc217 --save-temps foo.c -o foo
```

If we invoke `ls` again, we'll now see all the intermediate files in our directory:

```bash
$ ls
foo.c    foo.i    foo.s    foo.o    foo 
```

#### Halting the Build Process at Any Intermediate Stage

`gcc` provides command line options to halt the build process at any of the intermediate stages. Here's a breakdown of the options:

**`-E`:** This instructs `gcc` to halt the build process after the preprocessing stage. For example, if we invoke:

```bash
gcc217 -E foo.c
```

`gcc` will preprocess `foo.c` and halt. By default, the preprocessed output will be printed on stdout. To save the output in a `.i` file, we can use the `.o` option or the `>` redirection operator:

```bash
gcc217 -E foo.c -o foo.i
# or
gcc217 -E foo.c > foo.i
```

**`-S`:** This instructs `gcc` to halt the build process after compilation. The input can a `.c` file:

```bash
gcc217 -S foo.c
```

Or a `.i` file:

```bash
gcc217 -S foo.i
```

`gcc` will infer which stages to perform based on the file's extension--preprocessing and compilation for a `.c` file, and compilation only for a `.i` file. The output will automatically be saved in a `.s` file.

**`-c`:** This instructs `gcc` to halt the build process after assembly. As you might expect, the input can be a `.i`, `.c`, or `.s` file, and `gcc` will infer which stages to perform based on the file's extension. The output will automatically be saved in a `.o` file.

This `-c` option is by far the most commonly used `gcc` option to control the build process, so it pays to remember it. As we'll see in the chapter on Make, it is necessary for implementing incremental builds.&#x20;
