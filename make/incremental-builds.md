# How Incremental Builds Work in C

Take a look at the testintmath program shown in Figure X. We'll use this as a running example throughout this chapter, allowing us to demonste how incremental builds work.

<figure><img src="../.gitbook/assets/Screenshot 2024-07-22 at 6.19.25 PM.png" alt=""><figcaption><p>Figure X: testintmath program</p></figcaption></figure>

Recall the underlying process by which `testinmath` is built. The source files `intmath.c` and `testintmath.c` are _independently_ preprocessed, compiled, and assembled into object files `intmath.o` and `testintmath.o`, respectively. Of note is that in the preprocessing stage, headers specified via the `#include` directive are fetched and inserted into each file. To produce the executable `testintmath`, `intmath.o` and `testintmath.o` are linked--along with necessary object files from the C standard library. This multi-stage process is summarized in Figure X.

<figure><img src="../.gitbook/assets/Frame 31 (2).png" alt=""><figcaption><p>Figure X: GCC build process</p></figcaption></figure>

The key to incremental builds lies in caching object files and reusing them in subsequent builds when the source files they are derived from, or _depend_ on, haven't changed. From observing Figure X, the relationship between object files and source files should be apparent:  Each object file depends on its corresponding `.c` file and all `#included` headers. Specifically:

* `testintmath.o` depends on `testintmath.c`, `stdio.h`, `stdlib.h`, and `intmath.h`. (Actually, `testintmath.o` depends on many more header files, since `stdio.h` and `stdlib.h` themselves `#include` many header files).&#x20;
* `intmath.o` depends on `intmath.c` and `intmath.h`.

 (In practice, we need not be concerned with `stdio.h` and `stdlib.h` or any other system headers, since we don't modify them. Therefore, we'll ignore them for the remainder of this chapter.)

The most important thing to recognize is that changes to intmath.c do not impact testintmath.o, and changes to testintmath.c do not impact intmath.o. Therefore, changes to intmath.c do not necessitate rebuilding testintmath.o, and changes to testintmath.c do not necessitate rebuilding intmath.o. Let’s demonstrate this incremental build strategy in action. 

The first time we build `testintmath`, a full build is required; there’s no way around that. Importantly, however, we ensure to save the intermediately generated object files--`intmath.o` and `testintmath.o`--which by default `gcc` discards. How do we save object files? Recall the `-c` option, which tells `gcc` to halt the build process after the assembly stage and output object files. Thus, we build `testintmath` with the following two commands:

```
gcc -c intmath.c testintmath.c
gcc intmath.o testintmath.o -o testintmath
```

With the object files in hand, subsequent builds can be incremental. For example, suppose we modify `intmath.c`. To rebuild `testintmath`, we run `gcc -c` on `intmath.c` **only**, and then we link the newly created `intmath.o` with `testintmath.o` from the previous build:

```
gcc -c intmath.c
gcc intmath.o testintmath.o -o testintmath
```

This incremental build process is summarized in Figure X.

<figure><img src="../.gitbook/assets/Frame 31 (4).png" alt=""><figcaption><p>Figure X: Incremental build</p></figcaption></figure>

Similarly, suppose we modify `testintmath.c`. To rebuild `testintmath`, we run `gcc -c` on `testintmath.c` only, and then we link the newly created `testintmath.o` with `intmath.o` from the previous build:

```
gcc -c testintmath.c
gcc intmath.o testintmath.o -o testintmath
```

Suppose, however, that we were to modify `intmath.h`. This renders both `intmath.o` and `testintmath.o` obsolete, since `intmath.h` is #included in both their source files. As such, a full rebuild is required:

```
gcc -c intmath.c testintmath.c
gcc intmath.o testintmath.o -o testintmath
```

In general, changes to header file tend to be much more dramatic than changes to `.c` files, since header files, which serve as interfaces, are typically included in many `.c` files. For this reason, great caution should be taken before modifying a header file.

{% hint style="info" %}
It's important to understand that fundamentally, the underlying GCC build process is the same irrespective of whether we build our program via two commands:

```bash
gcc -c intmath.c testintmath.c
gcc intmath.o testintmath.o -o testintmath
```

Or via a single command:

```bash
gcc intmath.c testintmath.c -o testintmath
```

In both cases, `intmath.c` and `testintmath.c` will be independently preprocessed, compiled, and assembled into object files, which are then linked. The difference between these two approaches is that the two-command approach retains the object files while the single-command approach does not.
{% endhint %}
