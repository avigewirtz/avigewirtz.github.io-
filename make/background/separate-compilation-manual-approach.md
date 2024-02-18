# Separate compilation: Manual Approach

Suppose we just created the three source files and are building testintmath for the firs time.&#x20;

Rather than using the familiar command `gcc intmath.c testintmath.c -o testintmath`, which does not retain the resulting object files, we build our program in two steps. First, we invoke gcc on each .c file with the -c option, which tells GCC to generate object files, but not link them. We can invoke GCC on each .c file individually:

```
gcc -c intmath.c
gcc -c testintmath.c
```

Or we can invoke gcc on both files together:

```
gcc -c intmath.c testintmath.c
```

The result is the same. If you invoke ls, you'll see that you now have object files:

```
-> ls
intmath.c intmath.o testintmath.c testintmath.o
```

We need include intmath.h even though it is part of the source code for our program, since it is included by the preprocessor.&#x20;

The second step is to invoke GCC to link intmath.o and testintmath.o together. To specify that we want the executable to be named testintmath (rather than the default a.out), we use the -o option:&#x20;

```
gcc intmath.o testintmath.o -o testintmath
```

Becuase both files have .o extensions, GCC deduces that no compilation is needed, and thus begins goes immediately to linking. Note that GCC will also link necessary files from the C standard library, such as the the files which contain the printf() and scanf() functions.&#x20;

### Rebuilding testintmath

Suppose we make a change to intmath.c. To rebuild testintmath to incorporate the change, we only need to recompile intmath.c, and then we can link the updated intmath.o with the "old" testintmath.o to generate an updated executable. The process is identical if we were to make a change to only testintmath.c.&#x20;

If we were to change intmath.h, however, the effect would be much more dramatic. Since both intmath.c and testintmath.c "include" intmath.h,&#x20;

To be a little more formal, a file B is said to depend on a file A if a change in B requires A to be updated.

### Dependency graph

\<fill in>
