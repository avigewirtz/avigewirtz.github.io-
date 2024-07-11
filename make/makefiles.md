# Automating Incremental Builds With make

As we have seen, implementing incremental builds manually is possible but it requires some work. In particular, you have to:

1. Keep track of which source files (`.c` and `.h`) were modified since the last build.
2. Keep track of which object files (`.o`) are affected by the changes to the source files.
3. Run the commands to rebuild the program, in the correct order.

Even for a small program like `testintmath`, these tasks aren't particularly fun, though they are admittedly manageable. As programs grow larger, however, and the web of dependencies grows increasingly complex, these tasks quickly spiral out of control.

Consider a scenario where you modify header file `A`, which is `#included` in 20 `.c` files. To rebuild the program, you'd have to track down each of these `.c` files and recompile them. Worse yet, imagine header file `A` is also `#included` in header file `B`. You'd then have to also track down each of the `.c` files that `#include` `B` and recompile them as well.

It is precisely these sort of frustrations that led Stuart Feldman to create the `make` tool in 1976 while at Bell Labs. 

To make life easier (no pun intended), the `make` tool was developed, which automates this process. Here's a bird's eye view of how `make` works. It takes as input two pieces of information:&#x20;

1. The program's dependency graph. This is a directed graph that specifies the dependencies between the program's files as well as the commands to build each file from its dependencies.
2. The latest modification timestamp of each of the program's files.

`make` can obtain the files' timestamps on it's own from the filesystem. The dependency graph is provided through a user-written file known as a _makefile_, which we will describe how to create in the next section. Once an appropriate makefile is set up, the command:

```bash
make
```

is all it takes to incrementally build the program. `make` will analyze the makefile and, based on the files' dependencies and latest modification timestamps, determine the minimum set of files that need to be rebuilt to bring the program up to date.&#x20;
