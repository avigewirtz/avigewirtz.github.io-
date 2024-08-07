# How make Processes a Makefile

We've seen that we can build `testintmath` incrementally by simply invoking make. But how exactly does make figure out what to do? Let's examine the process in more detail to find out.

#### Core Algorithm

Bringing a file up-to-date is defined recursively as follows:

* First, bring its dependencies up to date.
* If the file is now older than any of its dependencies, or if it does not exist, execute its corresponding command(s).

The key point to recognize is that `make` cannot determine how to proceed with a file until it has processed all its dependencies. Because dependencies can themselves be targets with their own dependencies, this process is inherently recursive.&#x20;

Any traversal of the dependency graph in which each file's dependencies are processed before the file itself is a valid traversal. If you've taken COS226, one such traversal might immediately come to mind: depth-first search (DFS).&#x20;

Here's how the DFS traversal of the dependency graph works. \<fill in>.

Here is our dependency graph with each file labeled according to the order in which the DFS traversal encounters and processes it:&#x20;

<figure><img src="../.gitbook/assets/Group 263.png" alt="" width="563"><figcaption></figcaption></figure>

The pseudocode for a DFS traversal of the dependency graph is shown below. This algorithm relies on a function modtime which returns the last-modification time of a file or 0 if the file doesn't exist. This function marks a file as processed when the search backtracks from it. It uses a node- marking strategy to avoid both multiple updates for files that are the precursor of several files and infinite looping on dependency graphs containing cycles. The node marks do not affect the actual files, but instead are recorded in internal records about the file’s status. Note that the purpose of marking a file processed is to prevent processing a file twice (in our case, `intmath.h`). If an error occurs during the build process, the search halts and the error is reported. A file’s updating commands are executed after the search explores all edges leaving that node, so the ordering of files according to potential command execution gives a postorder listing of the DFS tree.

{% code lineNumbers="true" %}
```c
make(file)
{
    mark file as active
    for each of file’s dependencies (in order) {
        if (dependency is neither active nor processed) {
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
        if (commands fails) {
            exit_with_error;
        }
    }
    mark file as processed;
}
```
{% endcode %}

{% hint style="info" %}
This algorithm is not intended to be a faithful representation of the precise algorithm used by any implementation of make. It is simply intended to. Samples modification time before processing dependencies. Also, allows for phony targets. In this algorithm, won't work if&#x20;
{% endhint %}

To make things concrete, let's trace this DFS traversal at various stages of development.

#### Case 1: None of the Targets Exist

Assume we're building `testintmath` for the first time. Neither `testintmath` nor the object files (`testintmath.o` and `intmath.o`) exist yet. Here's a trace of the above shown algorithm in action. Note that I use arbitrary integers to represent the files' modification times (besides for 0, which indicates that the file doesn't exist).

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

The point to notice here is that even though all files are up-to-date, make still have to traverse the entire graph.&#x20;

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
