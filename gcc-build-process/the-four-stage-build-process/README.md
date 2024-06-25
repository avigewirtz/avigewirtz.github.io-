# Building Single-file Programs

We often view `gcc` as a black box. We pass it one or more C source files, and it outputs an executable. For example, suppose we have a C program contained within a single `.c` file, `foo.c`. To build our program with `gcc`, we run the following command:

```bash
gcc217 foo.c -o foo
```

And out comes the executable `foo`, which we can run by typing its name on the command line, prefixed by a `./`:

```bash
./foo
```

{% hint style="info" %}
Note that `-o foo` tells `gcc` to name the executable `foo`_,_ rather than the default name `a.out`.
{% endhint %}

If we take a look into this box, we see that the process takes place in a sequence of four phases, each of which transforms the program from one form into another, culminating in an executable. The phases are preprocessing, compilation, assembly, and linking. In fact, neither of these stages is performed by `gcc` itself. The programs that perform the build work are `cpp` (C preprocessor), `cc1` (C compiler), `as` (assembler), and `ld` (linker). `gcc` (that is, the `gcc` binary, typically stored in `/usr/bin`) is a relatively small driver program that serves as our interface to this toolchain. It parses our command line, figures out what we want to do, and then calls the aforementioned programs to do the actual work.&#x20;

Here's a bird's eye view of what happened under the hood when we ran gcc217 foo.c -o foo.&#x20;

1.  **Preprocessing stage.** First, `gcc` sends `foo.c` to the preprocessor. The preprocessor is a ... that performs basic modifications to the source code before compilation begins. The two main ones are:

    * **Removes comments.** Comments serve to help human readers understand the code, but they are of no use to the compiler. Hence, they can be discarded before compilation begins.
    * **Handles preprocessor directives.** These are lines in the code that begin with a `#` (hash). An example of a preprocessor directive is `#include` (e.g., `#include <stdio.h>`), which instructs the preprocessor to grab the contents of the specified file and paste it directly into the current file where the `#include` directive appears.

    The output of the preprocessor is `foo.i`.
2. **Compilation stage.** Next, gcc sends foo.i to the compiler (`cc1`). The compiler takes the preprocessed file `foo.i` and translates it into assembly language, producing a file called `foo.s`. Assembly language is a low-level representation of the program that is closer to machine code but still readable by humans.
3. **Assembly stage:** Next, gcc invokes the assembler on `foo.s`, generating an object file. This is a binary file format, containing machine code and metadata, typically in a file format called ELF.
4. **Linking stage:** Finally, gcc sends foo.o to the linker (ld). The linker combines `foo.o` with the necessary `.o` files from the C Standard Library, producing the _executable object file_ `foo`.

This process is summarized in Figure 4.

<figure><img src="../../.gitbook/assets/Frame 27 (5).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
A useful analogy is to think of the process as an assembly line, where the product is a C program, the tools are cpp, cc1, as, and ld, and the manager orchestrating the process is gcc. The program begins life as a source file stored in foo.c. As it goes through the assembly line, it gets worked by each of these tools, each transforming it one step closer to an executable. By the end, the produce emerges as an executable file, foo, ready to be loaded into memory and executed.
{% endhint %}

{% hint style="info" %}
**Note**

* In current GCC implementations, the preprocessor (`cpp`) is integrated into the compiler (`cc1`). The underlying sequence of operations is the same, but technically the first two build steps are performed by a single program (`cc1`).
* The build model we described assumes _static linking_, where all linking takes place before the file is executed. In practice, however, _dynamic linking_ might be used, where linking is performed when the file is executed.
{% endhint %}

#### Saving Intermediate Files

By default, `gcc` stores the intermediate files in `/tmp` and deletes them. Thus, if we invoke `ls` after building `foo`, we won't see any of the `.i`, `.s`, or `.o` files in our directory:

```bash
$ ls
foo.c
```

We can instruct `gcc` to save the intermediate files in the working directory by using the `--save-temps` option, like so:

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

**`-S`:** This instructs `gcc` to halt the build process after compilation. The input can be `.c` file(s) (e.g., `gcc217 -S foo.c`), `.i` file(s) (e.g., `gcc217 -S foo.i`), or even a mix of both (e.g., `gcc217 -S foo.c bar.i`). `gcc` will infer which stages to perform based on the file extension--preprocessing and compilation for `.c` files, and compilation only for `.i` files. The output will automatically be saved in `.s` files.

**`-c`:** This instructs `gcc` to halt the build process after assembly. As you might expect, the input can be `.i`, `.c`, or `.s` files, and `gcc` will infer which stages to perform based on the file extension. The output will automatically be saved in `.o` files.
