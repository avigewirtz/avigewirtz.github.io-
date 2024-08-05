# How make Processes a Makefile

We saw in the previous section that make make figures out what work to do to update the specified target. But how exactly does make figure out which commands to execute? Let's examine the execution in more detail to find out.&#x20;





Bringing a file up to date is defined recursively as follows. First, bring all of the file’s dependencies up to date. If the file is now older than one or more of its dependencies, or if it does not yet exist, then execute the command associated with the file.

The recursive update process can be performed by Algorithm 1.



```c
make(file)
{
    mark file as active;
    for each of file’s dependencies (in order) {
        if (the dependency is neither active nor processed) {
            make(dependency);
        }
    }
    m_time = modtime(file);
    for each of file’s dependencies {
        if (dependency is not active and modtime(dependency) > m_time) {
            record that file is out-of-date;
        }
    }
    if (file is out-of-date or m_time == 0) {
        execute file’s commands;
    }
    mark file as processed;
}
```







update performs a depth-first search> of the dependency graph. A node is marked active when first encountered and marked processed when the search backtracks from the node.







#### Case 1: None of the Targets Exist

Assume we're building `testintmath` for the first time. In other words, none of the target files (`testintmath`, `testintmath.o`, `intmath.o`) exist yet. Here's how processed the make file.&#x20;

First make notices that the command line contains no targets so it decides to make the default target, testintmath. It sees that testintmath does not exist. It checks for dependencies and sees two: testintmath.o and intmath.o. make now considers how to build testintmath.o and sees a rule for it. Again, it checks the dependencies, notices that count\_words.c has no rules but that the file exists, so make executes the commands to transform count\_words.c into count\_words.o by executing the command:



count\_words.o, lexer.o, and -lfl. make now considers how to build count\_words.o and sees a rule for it. Again, it checks the prerequisites, notices that count\_words.c has no rules but that the file exists, so make executes the commands to transform count\_words.c into count\_words.o by executing the command:It might seem that make should immediately invoke the command to build `testintmath` (i.e., `gcc217 testintmath.o intmath.o -o testintmath`) , but make must first ensure check for dependencies and ensure that `testintmath`'s dependencies&#x20;

* It starts off by examines the first target, `testintmath`. `make` notes that it does not exist. It might seem that make should immediately invoke the command to build it, but make must first ensure that its dependencies (i.e., `intmath.o`, `testintmath.o`) are up to date. In our case, they don't even exist yet.
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

Any traversal of the graph in which each file is processed only after its dependencies are processed is a valid traversal.

`make` processes a Makefile via a [depth first search](https://en.wikipedia.org/wiki/Depth-first\_search) (DFS) traversal of its dependency graph, starting from the default target or from the target specified on the command line. For each target, `make` recursively examines its dependencies, diving deeper until it reaches a leaf node (a file without any dependencies). During the traversal, it notes if each file exists, and if so, its timestamp. When it hits a leaf node, `make` backtracks to the previous target and checks any remaining dependencies.

During backtracking, it executes the command to build each target if either the target does not exist or if one of its deoendencies has a more recent modification timestamp.



If an error occurs during the execution of any command, `make` typically stops the build process and reports the error, although this behavior can be modified with flags such as `-k` to continue despite errors.

Let's now examine this DFS traversal at various points in development.

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
