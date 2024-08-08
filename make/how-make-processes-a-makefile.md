# How make Processes a Makefile

We've seen that we can build `testintmath` incrementally with `make`. But how exactly does `make` determine what actions to take? Let's examine the process in more detail to find out.

#### Core Algorithm

Bringing a file up-to-date is defined recursively as follows. First, bring its dependencies up-to-date. If the file is now older than any of its dependencies, or if it does not exist, execute its corresponding command(s). Because dependencies can themselves be targets with their own dependencies, this process is inherently recursive.

A simple algorithm for the recursive update process is shown below. You might recognize that this algorithm performs a [depth first search](https://en.wikipedia.org/wiki/Depth-first\_search) (DFS) traversal of the dependency graph. Files are marked "active" when first encountered and "processed" when the search backtracks from it. This marking strategy prevents infinite looping on cyclical dependency graphs and ensures that the same file isn't processed twice. The `modtime` function returns a file's last-modification time or 0 if the file does not exist.&#x20;

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

Here is our dependency graph with each file labeled according to the order in which the DFS traversal encounters and processes it:

<figure><img src="../.gitbook/assets/Group 263.png" alt="" width="563"><figcaption></figcaption></figure>

Notice that `intmath.h` is only processed once.&#x20;

{% hint style="info" %}
The algorithm shown above is not intended to faithfully represent the precise algorithm used by any implementation of `make`. It is simply intended to provide a high-level overview of the process. Actual `make` algorithms differ in at least two respects. First, they sample files' modification times before processing their dependencies, whereas our algorithm does so afterward. This distinction has subtle implications for performance and edge cases. Second, they allow [phony targets](makefile-version-2-phony-targets.md) to be dependencies, whereas our algorithm will fail in such cases.
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

Suppose we invoke `make` again immediately after building `testintmath`--in other words, when all files are up-to-date.

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

Observe that even though all files are up-to-date, make still have to traverse the entire graph.

#### Case 3: intmath.c is modified

Suppose we modify intmath.c but leave testintmath.c and intmath.h untouched.

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
