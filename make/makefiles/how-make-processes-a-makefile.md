# How make processes a Makefile

`make` processes a Makefile via a depth first search (DFS) traversal of its dependency graph, starting from the default target. Let's examine the traversal for our `testintmath` makefile at various points of development.&#x20;

## Case 1: Running our makefile when all the targets don't exist

Suppose we're building `testintmath` for the first time. In this case, neither `testintmath` nor `testintmath.o` and `intmath.o` exist yet. To build `testintmath`, we invoke:&#x20;

```
make
```

Here's how make processes the makefile:

* It starts off by examines the first target, `testintmath`. make notes that it does not exist. It might seem that make should immediately invoke the command to build `testintmath` (i.e., `gcc217 testintmath.o intmath.o -o testintmath`) , but make must first ensure that `testintmath`'s dependencies (i.e., `intmath.o`, `testintmath.o`) are up to date. In our case, they don't even exist yet.&#x20;
  * Make moves on to the rule for `testintmath.o`. It notes that `testintmath.o` too does not exist. Here too it might seem that make should immediately invoke the command to build `testintmath.o`, but make must first examine `testintmath.o`'s dependencies--`testinmath.c` and `intmath.h` are up to date. While this might be obvious to us, make has no way of knowing that `testintmath.c` and `intmath.h` exist and are up to date--meaning that they have no dependencies of their own that would require them to be rebuilt.
    * Make examines testintmath.c. It notes that it exists and is a leaf--meaning, it has no dependencies. Thus, it has no work to do for testintmath.c. It goes back to testintmath.o.
    * Make then examines intmath.h. It notes that it exists and is a leaf. It goes back to testintmath.o
  * At this point, make builds `testintmath.o` by invoking: `gcc217 -c testintmath.c`. It then goes back up to `testintmath`.&#x20;
  * Make now examines intmath.o. It notes that it does not exist.&#x20;
    * Make then examines intmath.c. It notes that it exists and is a leaf.&#x20;
    * Make sees that intmath.o's other dependency is intmath.h. It avoids a redundant check and instead goes back up to intmath.o
  * make now builds `intmath.o` by invoking: `gcc217 -c intmath.c`. It then goes back up to `testintmath`.&#x20;
* Finally, make builds `testintmath` by invoking: `gcc217 testintmath.o intmath.o -o testintmath`.

This sequence of operations is shown in Figure 2.4.

<figure><img src="../../.gitbook/assets/Group 66 (5).png" alt=""><figcaption></figcaption></figure>

## Case 2: Running our makefile when all targets are up to date

Suppose we invoke `make` immediately after building our program (i.e., when all files are up to date). The sequence of operations performed by make is shown in Figure 2.5.

<figure><img src="../../.gitbook/assets/Group 67 (1).png" alt=""><figcaption></figcaption></figure>

## Case 3: Running our makefile after a source file is modified

Suppose we invoke `make` after `intmath.c` is modified. The sequence of operations performed by make is shown in Figure 2.6.

<figure><img src="../../.gitbook/assets/Group 68 (2).png" alt=""><figcaption></figcaption></figure>
