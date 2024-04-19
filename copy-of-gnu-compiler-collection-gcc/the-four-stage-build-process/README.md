# The Big Picture

Suppose we have a program comprised of two .c file--foo.c and bar.c--and one header file, header.h, which is #included in both foo.c and bar.c. To build our program, we invoke the following command:&#x20;

```bash
gcc217 foo.c bar.c -o foobar
```

Assuming the build is succesful, that the `-o` option specifies that the executable be named _foobar,_ rather than the default name a.out. To run _foobar_, we simply invoke its pathname on the command line:

```
./foobar
```

Behind the scenes, quite a lot of work is involved in producing the executable. The sequence of operations is shown in Figure 4.2. Here's a breakdown of what happens at each stage:

1. **Preprocessing stage:** The preprocessor modifies the source code in _foo.c_ and _bar.c_ by including header files (stdio.h and header.h for foo.c, and header.h for bar.c), expanding macros, and removing comments. The output is of the preprocessor is stored in _foo.i_ and _bar.i_.
2. **Compilation stage:** The compiler translates _foo.i_ and _bar.i_ into assembly language files _testcircle.s_ and _circle.s._
3. **Assembly stage:** The assembler translates _foo.s_ and _bar.s_ into relocatable object files _foo.o_ and _bar.o_. These files contain machine code but are not executable.
4. **Linking stage:** The linker combines _foo.o_ and _bar.o_, along with necessary .o files from the C Standard Library, producing the executable file _foobar_.

<figure><img src="../../.gitbook/assets/Group 70.png" alt=""><figcaption></figcaption></figure>

Notice that the first three stages (preprocessing, compilation, and assembly) are performed on each file separately. Recognizing this is critical to understanding how the build process works.

### Saving Intermediate Files

By default, gcc does not retain the intermediate files (i.e., `.i`, `.s`, and `.o)`generated during the build process. Hence, if we invoke `ls` after building testcircle, we will not see any intermediate files:

```bash
> ls
bar.c    foo.c    foobar    header.h
```

We can instruct gcc to save the intermediate files by using the `--save-temps` option:

```
gcc217 --save-temps foo.c bar.c -o foobar
```

Invoking `ls`, we now see the intermediate files in our project directory:

```bash
> ls
bar.c    bar.i    bar.s    bar.o    foo.c    
foo.i    foo.s    foo.o    foobar   header.h
```

### Stopping the build process at any stage

GCC provides command line options to halt the build process after after any of the first three stages. Here's a breakdown of the options:

**`-E`: stop after preprocessing.** Example:`gcc -E foo.c bar.c`. By default, the preprocessed output will be printed on stdout, but you can save it to `.i` files instead using the `-o` option:

```
gcc -E foo.c -o foo.i
gcc -E bar.c -o bar.i
```

**`-S`: stop after compilation**. The input can be either .c or .i files.GCC will automatically save the assembly code in .s files. Examples:

```bash
gcc -S foo.c bar.c # preprocesses and compiles foo.c and bar.c
```

```bash
gcc -S foo.i bar.i # compiles foo.i andf bar.i
```

**`-S`: stop after assembly**. The input can be either .c, .i, or .o files. GCC will automatically save the object code in .o files. Examples:

```bash
gcc -c foo.c bar.c # preprocesses,compiles, and assembles foo.c and bar.c
```

```bash
gcc -c foo.i bar.i # compiles and assembles foo.i and bar.i
```

```
gcc -c foo.s bar.s # assembles foo.s and bar.s
```
