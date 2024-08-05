# How make Processes a Makefile

make's job is to bring file's up-to-date. Bringing a file up-to-date is defined recursively as follows. First, bring all of the file’s dependencies up to date. If the file is now older than any of its dependencies or does not exist, execute the command associated with the file.

The recursive update process can be performed by Algorithm 1. update performs a depth-first search of the dependency graph. A file is marked processed when the search backtracks from the file. The algorithm requires a function modtime that returns the last-modification time of a file. If the file does not exist, modtime returns 0.&#x20;

```c
make(file)
{
    for each of file’s dependencies (in order) {
        if (dependency is not processed) {
            make(dependency);
        }
    }
    m_time = modtime(file);
    for each of file’s dependencies {
        if (modtime(dependency) > m_time) {
            record that file is out-of-date;
        }
    }
    if (file is out-of-date or m_time == 0) {
        execute file’s commands;
    }
    mark file as processed;
}
```

To make things concrete, let's now examine this traversal at various points in development.&#x20;

#### Case 1: None of the Targets Exist

Assume we're building `testintmath` for the first time. In other words, none of the target files (`testintmath`, `testintmath.o`, `intmath.o`) exist yet. Here's how processed the make file.&#x20;





Let's walk through the make process for this case where none of the targets exist. We'll use the algorithm provided to update the `testintmath` target.

* make(`testintmath`)&#x20;
  * make(`testintmath.o`)&#x20;
    * make(`testintmath.c`)&#x20;
      * modtime(`testintmath.c`) = x.y.x
      * no action (source file, no associated command)&#x20;
      * mark testintmath.c as processed
    * make(`intmath.h`)&#x20;
      * modtime(`intmath.h`) = x.y.z
      * no action (source file, no associated command)&#x20;
      * mark intmath.h as processed
    * modtime(testintmath.o) = 0&#x20;
    * out of date. execute: gcc -c testintmath.c&#x20;
    * mark testintmath.o as processed&#x20;
  * make(intmath.o)&#x20;
    * make(intmath.c)&#x20;
      * modtime(intmath.c) = x.y.z
      * no action (source file, no associated command)&#x20;
      * mark intmath.c as processed
    * make(intmath.h) already processed, skip&#x20;
  * modtime(intmath.o) = 0&#x20;
  * execute: gcc -c intmath.c&#x20;
  * mark intmath.o as processed&#x20;
* modtime(testintmath) = 0&#x20;
* execute: gcc testintmath.o intmath.o -o testintmath&#x20;
* mark testintmath as processed

In this case, all commands are executed because none of the files exist. The order of execution is:

1. `gcc -c testintmath.c`
2. `gcc -c intmath.c`
3. `gcc testintmath.o intmath.o -o testintmath`

This creates all the object files and the final executable.



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
