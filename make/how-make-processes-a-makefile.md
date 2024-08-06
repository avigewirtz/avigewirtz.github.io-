# How make Processes a Makefile

We’ve seen that we can build testintmath incrementally by simply involing make. But how exactly does make figure out which commands (if any) to execute to being testintmath up-to-date? lets examine the execution in more detail to find out. 

#### Core Algorithm

Bringing a file up-to-date is defined recursively as follows. First, bring its dependencies up to date. If the file is now older than any of its dependencies or does not exist, bring it up-to-date by executing its corresponding command.

The key point to recognize is that make cannot determine how to proceed with a file
until it has ensured that its dependencies are up-to-date. Any traversal of the dependency graph in which each file's dependencies are processed before the file itself is a valid traverdal. If you've gaken COS226, one such traversal might immediately come to mind: depth-first search. Here's how it works. make begins the traversal from the default
target or the target specified on the command line. `make` recursively examines its dependencies, diving deeper until it reaches a file without any dependencies. make then processes the file, backtracks, and repeats the process. after make has finished preprocessing a file's dependencies, it checks if the file is older than any of its dependenies or doesnt exist. If so, it executes the file's command. 

The psuedocode for this algorithm is shown below. Thid algorithm relies on a function modtime which returns the last-modification time of a file or 0 if the file doesnt exist. Note that marking a file processed foes not affevt the file. The purpose is to prevent revisiting a file that has already been processed. In our case, it prevents make from processinf intmath.h twice. 

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
        if (commands fails) {
            exit_with_error;
        }
    }
    mark file as processed;
}
```

To make things concrete, let's trace this algorithm at various stages of development.

#### Case 1: None of the Targets Exist

Assume we're building `testintmath` for the first time. In other words, none of the target files (`testintmath`, `testintmath.o`, `intmath.o`) exist yet. Here's how make would process the dependency graph.

* <mark style="color:red;">make(</mark><mark style="color:red;">`testintmath`</mark><mark style="color:red;">)</mark>
  * <mark style="color:purple;">make(</mark><mark style="color:purple;">`testintmath.o`</mark><mark style="color:purple;">)</mark>
    * <mark style="color:green;">make(</mark><mark style="color:green;">`testintmath.c`</mark><mark style="color:green;">)</mark>
    * <mark style="color:green;">modtime(</mark><mark style="color:green;">`testintmath.c`</mark><mark style="color:green;">) = 1. Mark</mark> <mark style="color:green;">`testintmath.c`</mark> <mark style="color:green;">as processed</mark>
    * <mark style="color:green;">make(</mark><mark style="color:green;">`intmath.h`</mark><mark style="color:green;">)</mark>
    * <mark style="color:green;">modtime(</mark><mark style="color:green;">`intmath.h`</mark><mark style="color:green;">) = 2. Mark</mark> <mark style="color:green;">`intmath.h`</mark> <mark style="color:green;">as processed</mark>
  * <mark style="color:purple;">modtime(</mark><mark style="color:purple;">`testintmath.o`</mark><mark style="color:purple;">) = 0. Out-of-date. Execute:</mark> <mark style="color:purple;">`gcc -c testintmath.c`</mark><mark style="color:purple;">. Mark</mark> <mark style="color:purple;">`testintmath.o`</mark> <mark style="color:purple;">as processed</mark>
  * <mark style="color:purple;">make(</mark><mark style="color:purple;">`intmath.o`</mark><mark style="color:purple;">)</mark>
    * <mark style="color:green;">make(</mark><mark style="color:green;">`intmath.c`</mark><mark style="color:green;">)</mark>
    * <mark style="color:green;">modtime(</mark><mark style="color:green;">`intmath.c`</mark><mark style="color:green;">) = 3. Mark</mark> <mark style="color:green;">`intmath.c`</mark> <mark style="color:green;">as processed</mark>
      * <mark style="color:green;">Avoids redundant</mark> <mark style="color:green;"></mark><mark style="color:green;">`intmath.h`</mark> <mark style="color:green;"></mark><mark style="color:green;">check</mark>
  * <mark style="color:purple;">modtime(</mark><mark style="color:purple;">`intmath.o`</mark><mark style="color:purple;">) = 0. Out-of-date. Execute:</mark> <mark style="color:purple;">`gcc -c intmath.c`</mark><mark style="color:purple;">. Mark</mark> <mark style="color:purple;">`intmath.o`</mark> <mark style="color:purple;">as processed</mark>
* <mark style="color:red;">modtime(</mark><mark style="color:red;">`testintmath`</mark><mark style="color:red;">) = 0. Out-of-date. Execute:</mark> <mark style="color:red;">`gcc testintmath.o intmath.o - testintmath`</mark><mark style="color:red;">. Mark</mark> <mark style="color:red;">`testintmath`</mark> <mark style="color:red;">as processed</mark>

First make notices that the command line contains no targets so it decides to make the default target, testintmath. It sees that testintmath does not exist. It checks for dependencies and sees two: testintmath.o and intmath.o. make now considers how to build testintmath.o and sees a rule for it. Again, it checks the dependencies, notices that count\_words.c has no rules but that the file exists, so make executes the commands to transform count\_words.c into count\_words.o by executing the command:

count\_words.o, lexer.o, and -lfl. make now considers how to build count\_words.o and sees a rule for it. Again, it checks the prerequisites, notices that count\_words.c has no rules but that the file exists, so make executes the commands to transform count\_words.c into count\_words.o by executing the command:It might seem that make should immediately invoke the command to build `testintmath` (i.e., `gcc217 testintmath.o intmath.o -o testintmath`) , but make must first ensure check for dependencies and ensure that `testintmath`'s dependencies

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
