# Review of Compilation

As you know, in order to make a C program executable, you have to compile it, which converts it from its textual source code into machine code--the sequence of 1’s and 0’s that control the CPU of the computer. This conversion is performed by a compiler driver. GCC is a popular compiler driver for the C programming language and is the one used in COS217.&#x20;

### Compiling a single source file

To compile a single file, such as `hello.c`, we use the following command on armlab:

```
gcc217 hello.c
```

This converts `hello.c` into an executable file. By default, this file is named `a.out`. However, you can specify a different name for the executable by using the `-o` option. For example, to name the executable _hello_:

```
gcc217 hello.c -o hello
```

To run hello, simply type its [pathname](../linux/filesystem/pathnames.md) on the command line, like so:&#x20;

```
~> ./hello
Hello, world!
~> 
```

{% hint style="info" %}
Note that

`gcc217`&#x20;

is an alias for&#x20;

`gcc -Wall -Wextra -Wno-unused-parameter -ansi -pedantic`

This alias is set up in armlab but won't be recognized on other systems. To use the equivalent of `gcc217` on a different computer, you have two options: either set up such an alias on that computer or manually input the complete command that `gcc217` represents.

***

If you're curious, here's what each flag means:

* `-Wall`: Enable all the standard warning messages.
* `-Wextra`: Turn on additional warnings.
* `-Wno-unused-parameter`: Ignore warnings about unused parameters.
* `-ansi`: Ensure compliance with the ANSI standard for C.
* `-pedantic`: Enforce strict adherence to ISO standards.

This set of flags is chosen to encourage good coding practices, such as addressing potential issues before they become problematic and writing standard-compliant code.&#x20;
{% endhint %}

### Compiling multiple source files

If a program consists of multiple source files, you can generate an executable by specifying all filenames on the command line. For example, to generate an executable for the program consisting of file1.c, file2.c, and file3.c:

```
gcc217 file1.c file2.c file3.c -o executable_name
```

And GCC will generate the executable file.&#x20;
