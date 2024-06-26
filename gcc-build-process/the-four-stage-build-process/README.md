# The Big Picture

We often treat `gcc` as a black box. We pass it one or more C source files, and it outputs an executable file. If we look inside this box, however, we see that the underlying process takes place in a sequence of four phases--preprocessing, compilation, assembly, and linking. Each of these phases transforms the program from one form into another, culminating in an executable. Interestingly, none of these phases is performed by `gcc` binary itself. The programs that perform the work--collectively forming a toolchain--are `cpp` (C preprocessor), `cc1` (C compiler), `as` (assembler), and `ld` (linker). `gcc` is a driver program that serves as our interface to this toolchain. It parses our command line, figures out what we want to do, and then calls the appropriate programs to do the work.&#x20;

Consider a C program contained within a single `.c` file, `foo.c`. Running the command:

```bash
gcc217 foo.c -o foo
```

Results in an executable named `foo`, which we can run by typing its name on the command line, prefixed by a `./`:

```bash
./foo
```

{% hint style="info" %}
Note that `-o foo` tells `gcc` to name the executable `foo` rather than `a.out`, the default name for executables on Unix systems.
{% endhint %}

Here's a bird's eye view of what takes place under the hood:&#x20;

1. **Preprocessing phase.** First, `gcc` sends `foo.c` to the preprocessor (`cpp`). The preprocessor performs basic modifications to the source code, such as removing comments, inserting header files, and expanding macros. Note that the latter two operations are triggered by preprocessor directives--`#include` and `#define`, respectively. More on these directives in the next section. The output of the preprocessor is `foo.i`.&#x20;
2. **Compilation phase.** Next, `gcc` sends `foo.i` to the compiler (`cc1`). The compiler translates the preprocessed file `foo.i` into assembly language, producing a file called `foo.s`. Assembly language is a low-level representation of the program that is closer to machine code but still readable by humans.
3. **Assembly phase:**  `gcc` then send `foo.s` to the assembler (`as`), which translates it into machine code and stored the result in the object file `foo.o`. This is a binary file containing machine code and metadata.
4. **Linking phase:** Finally, `gcc` sends `foo.o` to the linker (`ld`). The linker then combines foo.o with the necessary .o files from the C standard library. Contains definitions of librayr functions called by foo.c, as well as generic starter code. The output is the executable file foo.&#x20;

This process is summarized in Figure 4.

<figure><img src="../../.gitbook/assets/Frame 27 (5).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
A useful analogy is to think of the process as an assembly line, where the product is a C program that begins as C source file and emerges as an executable file. The tools that work on the product are cpp, cc1, as, and ld, and the manager orchestrating the process is gcc.&#x20;
{% endhint %}

{% hint style="info" %}
**Note**

* In current GCC implementations, the preprocessor (`cpp`) is integrated into the compiler (`cc1`). The underlying sequence of operations is the same, but technically the first two build steps are performed by a single program (`cc1`).
* The build model we described assumes _static linking_, where all linking takes place before the file is executed. In practice, however, _dynamic linking_ might be used, where linking is performed when the file is executed.
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
