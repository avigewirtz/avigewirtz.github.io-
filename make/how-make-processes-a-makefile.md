# How make Processes a Makefile

We've seen that make executes the neccesary commands to bring targets up-to-date. But how exactly does make figure out which commands to execute? Let's examine the execution of our makefile in more detail to find out.&#x20;

<mark style="color:red;">How did make decide what to do? Let’s go over the previous execution in more detail to find out.</mark>

<mark style="color:red;">First make notices that the command line contains no targets so it decides to make the default goal, count\_words. It checks for prerequisites and sees three: count\_words.o, lexer.o, and -lfl. make now considers how to build count\_words.o and sees a rule for it. Again, it checks the prerequisites, notices that count\_words.c has no rules but that the file exists, so make executes the commands to transform count\_words.c into count\_words.o by executing the command:</mark>

```
     gcc -c count_words.c
```

<mark style="color:red;">This “chaining” of targets to prerequisites to targets to prerequisites is typical of how make analyzes a makefile to decide the commands to be performed.</mark>

<mark style="color:red;">The next prerequisite make considers is lexer.o. Again the chain of rules leads to lexer. c but this time the file does not exist. make finds the rule for generating lexer.c from lexer.l so it runs the flex program. Now that lexer.c exists it can run the gcc command.</mark>

<mark style="color:red;">Finally, make examines -lfl. The -l option to gcc indicates a system library that must be linked into the application. The actual library name indicated by “fl” is libfl.a. GNU make includes special support for this syntax. When a prerequisite of the form- l\<NAME> is seen, make searches for a file of the form libNAME.so; if no match is found, it then searches for libNAME.a. Here make finds /usr/lib/libfl.a and proceeds with the final action, linking.</mark>











As we saw, make’s job is to bring a target up-to-date. A target is considered up-to-date if it exists and it is newer than all it's dependencies.&#x20;

From POSIX: Before any target in the makefile is updated, each of its prerequisites (both explicit and implicit) shall be updated. This shall be accomplished by recursively processing each prerequisite. Upon recursion, each prerequisite shall become a target itself. Its prerequisites in turn shall be processed recursively until a target is found that has no prerequisites, or further recursion would require applying two inference rules one immediately after the other, at which point the recursion shall stop. As an extension, implementations may continue recursion when two or more successive inference rules need to be applied; however, if there are multiple different chains of such rules that could be used to create the target, it is unspecified which chain is used. The recursion shall then back up, updating each target as it goes.

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

<figure><img src="../.gitbook/assets/Group 66 (7).png" alt=""><figcaption></figcaption></figure>

#### Case 2: Running our makefile when all targets are up to date

Suppose we invoke `make` immediately after building `testintmath`. make will respond by notifying us that `testintmath` is up to date, and hence it will not execute any commands:

```bash
$ make
make: `testintmath' is up to date.
$
```

The DFS traversal is summarized in Figure 2.5.

<figure><img src="../.gitbook/assets/Group 67 (2).png" alt=""><figcaption></figcaption></figure>

#### Case 3: Running our makefile after a source file is modified

Suppose we invoke `make` after `intmath.c` is modified, but all the other files remain untouched. Make will execute the commands to build `intmath.o` and `testintmath`, but it will not execute the command to build `testintmath.o`:

```bash
$ make
gcc -c intmath.c
gcc testintmath.o intmath.o -o testintmath
$
```

The DFS traversal is summarized in Figure 2.6.

<figure><img src="../.gitbook/assets/Group 68 (4) (1).png" alt=""><figcaption></figcaption></figure>
