# How Incremental Builds Work in C

Recall the underlying process by which `testinmath` is built. `intmath.c` and `testintmath.c` are _independently_ preprocessed, compiled, and assembled into object files `intmath.o` and `testintmath.o`, respectively. Of note is that in the preprocessing stage, headers specified via the `#include` directive are fetched and inserted into each file `.c` file. Then, `intmath.o` and `testintmath.o` are linked--along with necessary object files from the C standard library--to produce the executable file `testintmath`. This multi-stage process is summarized in Figure X.&#x20;

<figure><img src="../.gitbook/assets/Frame 31 (2).png" alt=""><figcaption></figcaption></figure>

Notice that each object file is derived from, or _depends_ on, its corresponding .c file and #included headers only. It does not depend on any other source files. For example, intmath.o depends on intmath.c and intmath.h, but it does not depend on testintmath.c, stdio.h or stdlib.h. This means that changes to these source files have no impact on intmath.o. The key to incremental builds lies in caching object files and reusing them in subsequent builds when the source files they depend on haven't changed. For example, suppose testintmatj.c is modified but intmath.c and intmath.h are not. We rebuild testintmath by preproxessint, compiling, and assemnlimg intmatj.c only, and then linking tje nrwly generated intmath.o with testintmath.o from the previous build. Let’s demonstrate this incremental build strategy in action.&#x20;

The first time we build `testintmath`, we do a full build. There’s no way around that. Importantly, however, we ensure to save the intermediately generated object files--`intmath.o` and `testintmath.o`--which by default `gcc` discards. How do we save object files? Recall the `-c` option, which tells `gcc` to halt the build process after the assembly stage and output object files. Thus, we build `testintmath` with the following two commands:

```
gcc -c intmath.c testintmath.c
gcc intmath.o testintmath.o -o testintmath
```

With the object files in hand, subsequent builds can be incremental. For example, suppose we modify `intmath.c`. To rebuild `testintmath`, we run `gcc -c` on `intmath.c` **only**, and then we link the newly created `intmath.o` with `testintmath.o` from the previous build:&#x20;

```
gcc -c intmath.c
gcc intmath.o testintmath.o -o testintmath
```

This is summarized in Figure X.

<figure><img src="../.gitbook/assets/Frame 34.png" alt="" width="563"><figcaption></figcaption></figure>

Similarly, suppose we modify `testintmath.c`. To rebuild `testintmath`, we run `gcc -c` on `testintmath.c` only, and then we link the newly created `testintmath.o` with `intmath.o` from the previous build:&#x20;

```
gcc -c testintmath.c
gcc intmath.o testintmath.o -o testintmath
```

Suppose, however, that we were to modify `intmath.h`. This renders both `intmath.o` and `testintmath.o` obsolete, since `intmath.h` is included in both their source files. Thus, we'd have to do a full rebuild:

```
gcc -c intmath.c testintmath.c
gcc intmath.o testintmath.o -o testintmath
```

{% hint style="info" %}
It's important to understand that fundamentally, the underlying GCC build process is the same irrespective of whether we build our program via two commands:

```bash
gcc217 -c intmath.c testintmath.c
gcc217 intmath.o testintmath.o -o testintmath
```

Or via a single command:

```bash
gcc217 intmath.c testintmath.c -o testintmath
```

In both cases, `intmath.c` and `testintmath.c` will be independently preprocessed, compiled, and assembled into object files, which are then linked. The difference between these two approaches is that the two-command approach retains the object files while the single-command approach does not.
{% endhint %}
