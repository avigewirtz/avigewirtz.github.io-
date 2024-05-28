# Linker and Preprocessor

* Imagine you're a compiler designer. Goal is to build a compilation system that can take n C source files as input and output a single file that can be loaded into memory and executed.
* The first approach is to build all n source files as a monolithic unit. Source code in all files would be combined and then translated into machine code. Second approach is to treat each source file as an independent unit, translate each source file separately into machine code and then link the machine code together.

<figure><img src="../.gitbook/assets/Group 206 (1).png" alt=""><figcaption></figcaption></figure>



gcc takes these n files as input and produces as output a single file that can be loaded into memory and executed. At some point, all the code modules must have been combined together. When is this done? Consider two approaches compiler designers might take to&#x20;

Put yourself in the shoes of a compiler designer.&#x20;

Consider two apraoches to build this program. One approach is to first combine all source files into a single, monolithic unit and then translate that unit into machine code. This file can be loaded into memory as is and executed. Second appraoch would be to translate each source file independently into machine code and then combine the machine code units into a unified file?



This method would admittedly present some challenges relating to implementing scoping and the like, but we can devise clever solutions for these. The main problem with this approach is that the entire program must be recompiled whenever any change is made, no matter how small. This would be incredibly time-consuming and inefficient, especially for large projects. The approach C compilers actually use is to first compile each source file separately into its own machine code file, known as a **relocatable object file**. A separate program called the **linker** then combines all the relocatable object files, including those from the C standard library, to generate the final, executable object file.

The approach C compilers use is to first compile each source file separately into its own machine code file, known as a **relocatable object file**. A separate program called the **linker** then combines all the relocatable object files, including those from the C standard library, to generate a final, **executable object file**.&#x20;

#### Challenges of Separate Compilation

Separate compilation addresses several challenges. One key issue is type checking. In a separate compilation scheme, the compiler processes one file at a time. For example, consider a program composed of two files, `foo.c` and `bar.c`. When the compiler processes `foo.c`, it has no knowledge of the contents of `bar.c` or even that it exists at all. It only looks at `foo.c`.

Consider the following scenario:

```c
int main() {
    bar(1, 2.1);
    return 0;
}
```

Here, `foo.c` calls the `bar` function, which is defined in `bar.c`. The problem is that when compiling `foo.c`, the compiler doesn't know what the function `bar` is. It doesn't know its return type, nor does it know that it takes two arguments—an `int` and a `double`. It has no way of type checking. The compiler might let it slide, as was the case in C80/C90, where it assumed the function was called correctly and returned an `int`. This proved to be extremely error-prone, which is why C99 prohibits calling a function in this manner.

The solution is to insert prototypes of all functions called at the top of the file. When the compiler processes `foo.c`, it sees:

```c
void bar(int i, double j);

int main() {
    bar(int 1, double 2);
    return 0;
}
```

The prototype is our way of telling the compiler that we have a function named `bar` that takes an `int` and a `double` as arguments and returns nothing. Now, when we make the call, the compiler can type-check it.

Even if the function we're calling is from the C Standard Library, we also have to declare it first. The compiler does not have any internal table of library prototypes it consults whenever it encounters a call to a library function. Instead, it is on the programmer to declare them first. For example, if we amend `foo.c` by adding a `printf` statement, we'd have to declare the `printf` function before making the call:

```c
int printf(const char *format, ...);
void bar(int i, double j);

int main() {
    bar(int 1, double 2);
    printf("hello");
    return 0;
}
```

#### The Preprocessor

When C was created, prototypes for each externally defined function had to be manually typed out. This approach has a couple of issues. First, if the programmer used, say, 20 I/O functions from the C library, they would have to type out each prototype. This is obviously tedious. Second, if one of the definitions changes and the prototype no longer matches, the programmer might not even know that it changed. The code would compile and link without error, but have a runitme error like a segmentation fault.&#x20;

The solution is to extend C by adding a file inclusion mechanism, where we store prototypes of related functions, such as all C library I/O functions, in a single file elsewhere, and then have them inserted into the current file automatically before compilation begins. This way, including many prototypes is easy, and if one changes, it will be updated in the source file automatically.

File inclusion was added by means of a preprocessor, a program that modifies the source code before actual compilation begins. To insert a file, you add an `#include` directive at the beginning of the file, specifying the name of a file the preprocessor should insert into the current file. The inserted file is known as a header file, by convention with a `.h` suffix, so called because its contents are typically inserted at the head of the file.
