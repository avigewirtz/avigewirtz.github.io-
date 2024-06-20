# The Big Picture

Suppose we have a C program contained within a single `.c` file, `foo.c`. To build our program with `gcc`, we run the following command:

```bash
gcc217 foo.c -o foo
```

{% hint style="info" %}
Note that `-o foo` tells `gcc` to the executable `foo`_,_ rather than the default name `a.out`.
{% endhint %}

To run `foo`, we type its name on the command line, prefixed by a `./`:

```bash
./foo
```

#### Under the Hood

Under the hood, quite a lot of work is involved in producing the executable foo. It can be broken down into four main stages: preprocessing, compilation, assembly, and linking. The programs that perform these stages are `cpp` (C preprocessor), `cc1` (C compiler), `as` (assembler), and `ld` (linker), respectively. The `gcc` binary is actually just a relatively small driver program. It parses the command line, determines what you want to do, and calls the aforementioned programs to do the actaul build work. When you run the command `gcc foo.c -o foo`, `gcc` calls each of these four programs programs in sequence on your behalf, passing the output of each program as input to the next.&#x20;

Here's a bird's eye view of what happens at each stage:

1.  **Preprocessing stage.** First, `gcc` sends foo.c to the preprocessor, cpp. The preprocessor modifies the source code in `foo.c` in two key ways:&#x20;

    * **Removes comments.** Comments serve to help human readers understand the code, but they are of no use to the compiler. Hence, they can be discarded before compilation begins.
    * **Handles preprocessor directives.** These are lines in the code that begin with a `#` (hash). An example of a preprocessor directive is `#include` (e.g., `#include <stdio.h>`), which instructs the preprocessor to grab the contents of the specified file and paste it directly into the current file where the `#include` directive appears.

    The output of the preprocessor is `foo.i`.
2. **Compilation stage.** Next, gcc sends foo.i to the compiler (`cc1`). The compiler takes the preprocessed file `foo.i` and translates it into assembly language, producing a file called `foo.s`. Assembly language is a low-level representation of the program that is closer to machine code but still readable by humans.
3. **Assembly stage:** After that, the assembler (`as`) converts the assembly language in `foo.s` into machine code, creating a relocatable object file named `foo.o`.
4. **Linking stage:** Finally, gcc sends foo.o to the linker (ld). The linker combines `foo.o` with the necessary `.o` files from the C Standard Library, producing the _executable object file_ `foo`.&#x20;

A useful analogy is to think of the process as an assembly line, where the product is a C program, the tools are cpp, cc1, as, and ld, and the manager orchestrating the process is gcc. Each stage transforms the source code into a more refined form until it eventually becomes an executable file. You can see this full sequence of operations by invoking `gcc` with the `-v` (verbose) option. You will gain a much greater appreciation of the role the `gcc` driver program plays in simplifying the build process.

<figure><img src="../../.gitbook/assets/Frame 27 (5).png" alt=""><figcaption></figcaption></figure>

The critical point to recognize is that definitions of library functions called in `foo.c` are resolved at link time. We will see the practical implications of this in the next section.

{% hint style="info" %}
**Note**

* In current GCC implementations, the preprocessor (`cpp`) is integrated into the compiler (`cc1`). The underlying sequence of operations is the same, but technically the first two build steps are performed by a single program (`cc1`).
* The build model we described assumes _static linking_, where all linking takes place before runtime. In practice, however, _dynamic linking_ might be used, where linking is performed during execution of the program.
{% endhint %}

#### Saving Intermediate Files

By default, `gcc` stores the intermediate files in `/tmp` and deleted by gcc. Thus, if we invoke `ls` after building `foobar`, for example, we won't see any of the `.i`, `.s`, or `.o` files in our directory:

```bash
$ ls
bar.c    foo.c    foobar
```

We can instruct `gcc` to save the intermediate files in the working directory by using the `--save-temps` option, like so:

```bash
gcc217 --save-temps foo.c bar.c -o foobar
```

If we invoke `ls` again, we'll now see all the intermediate files in the working directory:

```bash
$ ls
bar.c    bar.i    bar.s    bar.o    foo.c    
foo.i    foo.s    foo.o    foobar   
```

#### Halting the Build Process at Any Intermediate Stage

By default, `gcc` performs all four stages of the build process. However, it provides command line options to halt the build process at any of the intermediate stages. Here's a breakdown of the options:

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

#### Building a Multi-file C Program

As we know, the source code of a C program may be distributed across any number of files. Suppose we divide our program into two `.c` files, `foo.c`, and `bar.c`. We build our program by supplying both files as arguments to `gcc217`:

```bash
gcc217 foo.c bar.c -o foobar
```

The sequence of operations performed by `gcc` is summarized in Figure 12. The critical point to recognize here is that the first three stages of the build process (i.e., preprocessing, compilation, and assembly) are performed on each file independently. Thus, definitions in foo.\* are not visible to the compiler when its processing bar.\*, and vice versa. Here too, the definitions are resolved at link time.

<figure><img src="../../.gitbook/assets/Frame 29.png" alt=""><figcaption></figcaption></figure>
