# Running make

The basic syntax to run `make` is:

```bash
make target
```

where `target` is the name of the file you want make to build (see, however, [phony targets](../makefile-version-2-phony-targets.md)). If you omit a target, `make` defaults to the first target in the Makefile. In our case, that's `testintmath`. Thus, the command:

```bash
make
```

Is equivalent to:

```bash
make testintmath
```

In both cases, `make` will attempt to build `testintmath`. If `testintmath` is either out of date or does not exist, `make` will execute the commands needed to bring `testintmath` up to date. By default, `make` prints each of the commands it executes. Say we run `make` when all targets are out of date or do not exist. The output will look like this:

```bash
$ make
gcc -c testintmath.c
gcc -c intmath.c
gcc testintmath.o intmath.o -o testintmath
$
```

If we run `make` again immediately afterward, it will detect that `testintmath` is up to date and not execute any commands:

```bash
$ make
make: `testintmath' is up to date.
$
```

{% hint style="info" %}
It's important to recognize that `make` does not read a Makefile from top to bottom, processing all rules within it. It starts with the first rule or the rule specified on the command line and then processes only the rules that are reachable from it. So, for example, if we run:

```bash
make intmath.o
```

make will process the rule for `intmath.o` only. It will not process the rules for `testintmath.o` or `testintmath`, since they are not reachable from it.
{% endhint %}















As we saw, make’s job is to bring a target up-to-date. A target is considered up-to-date if it exists and it is newer than all it's dependencies.&#x20;



In order for make to bring a target up-to-date, make must first ensure that the target’s dependencies are up-to-date. A target is considered up-to-date if it exists and it has no dependencies with newer timestamps.&#x20;



For example, in order to bring testintmath up-to-date, make must first ensure that testintmath.o and intmath.o are up-to-date. Thus, make must examine these targets before determining how to proceed with testintmath.

Any traversal of the graph in which each file is processed only after its dependencies are processed is a valid traversal.

`make` processes a Makefile via a [depth first search](https://en.wikipedia.org/wiki/Depth-first\_search) (DFS) traversal of its dependency graph, starting from the default target or from the target specified on the command line. For each target, `make` recursively examines its dependencies, diving deeper until it reaches a leaf node (a file without any dependencies). During the traversal, it notes if each file exists, and if so, its timestamp. When it hits a leaf node, `make` backtracks to the previous target and checks any remaining dependencies.

During backtracking, it executes the command to build each target if either the target does not exist or if one of its deoendencies has a more recent modification timestamp.

This DFS traversal ensures that all of a target's dependencies exist and are up to date before building it.

If an error occurs during the execution of any command, `make` typically stops the build process and reports the error, although this behavior can be modified with flags such as `-k` to continue despite errors.

Let's now examine this DFS traversal at various points in development.

#### Case 1: Running our makefile when all the targets don't exist

Suppose we're building `testintmath` for the first time. In this case, neither `testintmath,` `testintmath.o`, or `intmath.o` exist. Here's how `make` would process the Makefile if we were to run:

```
make
```

* It starts off by examines the first target, `testintmath`. `make` notes that it does not exist. It might seem that make should immediately invoke the command to build `testintmath` (i.e., `gcc217 testintmath.o intmath.o -o testintmath`) , but make must first ensure that `testintmath`'s dependencies (i.e., `intmath.o`, `testintmath.o`) are up to date. In our case, they don't even exist yet.
  * `make` moves on to `testintmath.o`. It notes that `testintmath.o` does not exist.
    * `make` examines `testintmath.c`. It notes that it exists and is a leaf--meaning, it has no dependencies. Thus, it has no work to do for `testintmath.c`. `make` then backtracks to `testintmath.o`.
    * `make` examines `intmath.h`. It notes that it exists and is a leaf. `make` then backtracks again to `testintmath.o`.
  * Having determined that `testintmath.o`'s dependencies exist and are up to date, `make` now builds `testintmath.o` by invoking: `gcc217 -c testintmath.c`. It then backtracks to `testintmath`.
  * `make` now examines testintmath's other dependency--intmath.o. It notes that it does not exist.
    * `make` then examines intmath.c. It notes that it exists and is a leaf.
    * `make` sees that intmath.o's other dependency is intmath.h. It avoids a redundant check and instead goes back up to intmath.o
  * `make` now builds `intmath.o` by invoking: `gcc217 -c intmath.c`. It then goes back up to `testintmath`.
* Finally, `make` builds `testintmath` by invoking: `gcc217 testintmath.o intmath.o -o testintmath`.

The DFS traversal is summarized in Figure 2.4.

<figure><img src="../../.gitbook/assets/Group 66 (7).png" alt=""><figcaption></figcaption></figure>

#### Case 2: Running our makefile when all targets are up to date

Suppose we invoke `make` immediately after building `testintmath`. make will respond by notifying us that `testintmath` is up to date, and hence it will not execute any commands:

```bash
$ make
make: `testintmath' is up to date.
$
```

The DFS traversal is summarized in Figure 2.5.

<figure><img src="../../.gitbook/assets/Group 67 (2).png" alt=""><figcaption></figcaption></figure>

#### Case 3: Running our makefile after a source file is modified

Suppose we invoke `make` after `intmath.c` is modified, but all the other files remain untouched. Make will execute the commands to build `intmath.o` and `testintmath`, but it will not execute the command to build `testintmath.o`:

```bash
$ make
gcc -c intmath.c
gcc testintmath.o intmath.o -o testintmath
$
```

The DFS traversal is summarized in Figure 2.6.
