# How make Processes a Makefile

We've seen that we can build `testintmath` incrementally by simply invoking make. But how exactly does make figure out what to do? Let's examine the process in more detail to find out.

#### Core Algorithm

Bringing a file up-to-date is defined recursively as follows:

* First, bring its dependencies up to date.
* If the file is now older than any of its dependencies, or if it does not exist, execute its corresponding command(s).

The key point to recognize is that `make` cannot determine how to proceed with a file until it has ensured that its (direct and transitive) dependencies are up-to-date. Any traversal of the dependency graph in which each file's dependencies are processed before the file itself is a valid traversal. If you've taken COS226, one such traversal might immediately come to mind: depth-first search (DFS).

Here's how the DFS traversal of the dependency graph works. `make` begins the traversal from the default target or the target specified on the command line. `make` recursively examines its dependencies, diving deeper until it reaches a file without any dependencies. `make` then processes the file, backtracks to the parent file, and repeats the process for any remaining dependencies. After `make` has finished preprocessing a file's dependencies, it checks if the file is older than any of its dependencies or doesn't exist. If so, it executes the file's command. If an error occurs during the execution of any command, `make` typically stops the build process and reports the error, although this behavior can be modified with flags such as `-k` to continue despite errors.

<figure><img src="../.gitbook/assets/Group 263.png" alt="" width="563"><figcaption></figcaption></figure>

The pseudocode for this algorithm is shown below. This algorithm relies on a function modtime which returns the last-modification time of a file or 0 if the file doesn't exist. This function marks a file as processed when the search backtracks from it. Note that this does not affect the file. It's simply for internal record-keeping to prevent revisiting a file that has already been processed. In our case, it prevents make from processing `intmath.h` twice.

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

Assume we're building `testintmath` for the first time. In other words, none of the target files (`testintmath`, `testintmath.o`, `intmath.o`) exist yet. Here's how make processes the dependency graph. Note that I'm using arbitrary integers to represent the files' modification times (besides for 0, which indicates that the file doesn't exist).

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
    * <mark style="color:green;">Avoids redundant</mark> <mark style="color:green;">`intmath.h`</mark> <mark style="color:green;">check</mark>
  * <mark style="color:purple;">modtime(</mark><mark style="color:purple;">`intmath.o`</mark><mark style="color:purple;">) = 0. Out-of-date. Execute:</mark> <mark style="color:purple;">`gcc -c intmath.c`</mark><mark style="color:purple;">. Mark</mark> <mark style="color:purple;">`intmath.o`</mark> <mark style="color:purple;">as processed</mark>
* <mark style="color:red;">modtime(</mark><mark style="color:red;">`testintmath`</mark><mark style="color:red;">) = 0. Out-of-date. Execute:</mark> <mark style="color:red;">`gcc testintmath.o intmath.o - testintmath`</mark><mark style="color:red;">. Mark</mark> <mark style="color:red;">`testintmath`</mark> <mark style="color:red;">as processed</mark>

#### Case 2: All targets up up-to-date

Suppose we invoke `make` immediately after building `testintmath`.

* <mark style="color:red;">make(</mark><mark style="color:red;">`testintmath`</mark><mark style="color:red;">)</mark>
  * <mark style="color:purple;">make(</mark><mark style="color:purple;">`testintmath.o`</mark><mark style="color:purple;">)</mark>
    * <mark style="color:green;">make(</mark><mark style="color:green;">`testintmath.c`</mark><mark style="color:green;">)</mark>
    * <mark style="color:green;">modtime(</mark><mark style="color:green;">`testintmath.c`</mark><mark style="color:green;">) = 1. Mark</mark> <mark style="color:green;">`testintmath.c`</mark> <mark style="color:green;">as processed</mark>
    * <mark style="color:green;">make(</mark><mark style="color:green;">`intmath.h`</mark><mark style="color:green;">)</mark>
    * <mark style="color:green;">modtime(</mark><mark style="color:green;">`intmath.h`</mark><mark style="color:green;">) = 2. Mark</mark> <mark style="color:green;">`intmath.h`</mark> <mark style="color:green;">as processed</mark>
  * <mark style="color:purple;">modtime(</mark><mark style="color:purple;">`testintmath.o`</mark><mark style="color:purple;">) = 4. Up-to-date.</mark> <mark style="color:purple;">Mark</mark> <mark style="color:purple;">`testintmath.o`</mark> <mark style="color:purple;">as processed</mark>
  * <mark style="color:purple;">make(</mark><mark style="color:purple;">`intmath.o`</mark><mark style="color:purple;">)</mark>
    * <mark style="color:green;">make(</mark><mark style="color:green;">`intmath.c`</mark><mark style="color:green;">)</mark>
    * <mark style="color:green;">modtime(</mark><mark style="color:green;">`intmath.c`</mark><mark style="color:green;">) = 3. Mark</mark> <mark style="color:green;">`intmath.c`</mark> <mark style="color:green;">as processed</mark>
    * <mark style="color:green;">Avoids redundant</mark> <mark style="color:green;">`intmath.h`</mark> <mark style="color:green;">check</mark>
  * <mark style="color:purple;">modtime(</mark><mark style="color:purple;">`intmath.o`</mark><mark style="color:purple;">) = 5. Up-to-date. Mark</mark> <mark style="color:purple;">`intmath.o`</mark> <mark style="color:purple;">as processed</mark>
* <mark style="color:red;">modtime(</mark><mark style="color:red;">`testintmath`</mark><mark style="color:red;">) = 6.</mark> <mark style="color:red;">Up-to-date. Mark</mark> <mark style="color:red;">`testintmath`</mark> <mark style="color:red;">as processed</mark>

#### Case 3: intmath.c is modified

Suppose we invoke `make` after `intmath.c` is modified, but all the other files remain untouched.

* <mark style="color:red;">make(</mark><mark style="color:red;">`testintmath`</mark><mark style="color:red;">)</mark>
  * <mark style="color:purple;">make(</mark><mark style="color:purple;">`testintmath.o`</mark><mark style="color:purple;">)</mark>
    * <mark style="color:green;">make(</mark><mark style="color:green;">`testintmath.c`</mark><mark style="color:green;">)</mark>
    * <mark style="color:green;">modtime(</mark><mark style="color:green;">`testintmath.c`</mark><mark style="color:green;">) = 1. Mark</mark> <mark style="color:green;">`testintmath.c`</mark> <mark style="color:green;">as processed</mark>
    * <mark style="color:green;">make(</mark><mark style="color:green;">`intmath.h`</mark><mark style="color:green;">)</mark>
    * <mark style="color:green;">modtime(</mark><mark style="color:green;">`intmath.h`</mark><mark style="color:green;">) = 2. Mark</mark> <mark style="color:green;">`intmath.h`</mark> <mark style="color:green;">as processed</mark>
  * <mark style="color:purple;">modtime(</mark><mark style="color:purple;">`testintmath.o`</mark><mark style="color:purple;">) = 4. Up-to-date. Mark</mark> <mark style="color:purple;">`testintmath.o`</mark> <mark style="color:purple;">as processed</mark>
  * <mark style="color:purple;">make(</mark><mark style="color:purple;">`intmath.o`</mark><mark style="color:purple;">)</mark>
    * <mark style="color:green;">make(</mark><mark style="color:green;">`intmath.c`</mark><mark style="color:green;">)</mark>
    * <mark style="color:green;">modtime(</mark><mark style="color:green;">`intmath.c`</mark><mark style="color:green;">) = 7. Mark</mark> <mark style="color:green;">`intmath.c`</mark> <mark style="color:green;">as processed</mark>
    * <mark style="color:green;">Avoids redundant</mark> <mark style="color:green;">`intmath.h`</mark> <mark style="color:green;">check</mark>
  * <mark style="color:purple;">modtime(</mark><mark style="color:purple;">`intmath.o`</mark><mark style="color:purple;">) = 5. Out-of-date (older than intmath.c). Execute:</mark> <mark style="color:purple;">`gcc -c intmath.c`</mark><mark style="color:purple;">. Mark</mark> <mark style="color:purple;">`intmath.o`</mark> <mark style="color:purple;">as processed</mark>
* <mark style="color:red;">modtime(</mark><mark style="color:red;">`testintmath`</mark><mark style="color:red;">) = 6. Out-of-date (older than newly updated intmath.o). Execute:</mark> <mark style="color:red;">`gcc testintmath.o intmath.o - testintmath`</mark><mark style="color:red;">. Mark</mark> <mark style="color:red;">`testintmath`</mark> <mark style="color:red;">as processed</mark>
