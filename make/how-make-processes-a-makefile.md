# How make Processes a Makefile

`make` processes a Makefile via a [depth first search](https://en.wikipedia.org/wiki/Depth-first\_search) (DFS) traversal of its dependency graph, starting from the default target. Let's examine the traversal for our `testintmath` makefile at various points of development.&#x20;

### Case 1: Running our makefile when all the targets don't exist

Suppose we're building `testintmath` for the first time. In this case, neither `testintmath` nor `testintmath.o` and `intmath.o` exist yet. To build `testintmath`, we invoke:&#x20;

```bash
$ make
gcc -c testintmath.c
gcc -c intmath.c
gcc testintmath.o intmath.o -o testintmath
$
```

Here's how `make` processes the Makefile:

* It starts off by examines the first target, `testintmath`. `make` notes that it does not exist. It might seem that make should immediately invoke the command to build `testintmath` (i.e., `gcc217 testintmath.o intmath.o -o testintmath`) , but make must first ensure that `testintmath`'s dependencies (i.e., `intmath.o`, `testintmath.o`) are up to date. In our case, they don't even exist yet.&#x20;
  * `make` moves on to `testintmath.o`. It notes that `testintmath.o` does not exist.&#x20;
    * `make` examines `testintmath.c`. It notes that it exists and is a leaf--meaning, it has no dependencies. Thus, it has no work to do for `testintmath.c`. `make` then backtracks to `testintmath.o`.
    * `make` examines `intmath.h`. It notes that it exists and is a leaf. `make` then backtracks again to `testintmath.o`.
  * Having determined that `testintmath.o`'s dependencies exist and are up to date, `make` now builds `testintmath.o` by invoking: `gcc217 -c testintmath.c`. It then backtracks to `testintmath`.&#x20;
  * `make` now examines testintmath's other dependency--intmath.o. It notes that it does not exist.&#x20;
    * `make` then examines intmath.c. It notes that it exists and is a leaf.&#x20;
    * `make` sees that intmath.o's other dependency is intmath.h. It avoids a redundant check and instead goes back up to intmath.o
  * `make` now builds `intmath.o` by invoking: `gcc217 -c intmath.c`. It then goes back up to `testintmath`.&#x20;
* Finally, `make` builds `testintmath` by invoking: `gcc217 testintmath.o intmath.o -o testintmath`.

The DFS traversal is summarized in Figure 2.4.

<figure><img src="../.gitbook/assets/Group 66 (7).png" alt=""><figcaption></figcaption></figure>

### Case 2: Running our makefile when all targets are up to date

Suppose we invoke `make` immediately after building `testintmath`. make will respond by notifying us that `testintmath` is up to date, and hence it will not execute any commands:&#x20;

```bash
$ make
make: `testintmath' is up to date.
$
```

The DFS traversal is summarized in Figure 2.5.

<figure><img src="../.gitbook/assets/Group 67 (2).png" alt=""><figcaption></figcaption></figure>

### Case 3: Running our makefile after a source file is modified

Suppose we invoke `make` after `intmath.c` is modified, but all the other files remain untouched. Make will execute the commands to build `intmath.o` and `testintmath`, but it will not execute the command to build `testintmath.o`:

```bash
$ make
gcc -c intmath.c
gcc testintmath.o intmath.o -o testintmath
$
```

The DFS traversal is summarized in Figure 2.6.

<figure><img src="../.gitbook/assets/Group 68 (4) (1).png" alt=""><figcaption></figcaption></figure>
