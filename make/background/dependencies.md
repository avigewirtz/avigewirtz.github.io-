# Dependencies



## Direct Dependencies

You'd be hard pressed to find a self contained C program

These are the most straightforward kind of dependencies. If file A directly includes a header file B or directly uses a function from an object file or library C, then A has direct dependencies on B and C. Consider the following three files: `intmath.h`, `intmath.c`, and `testintmath.c`.&#x20;

**File `intmath.h`:**

```c
#ifndef INTMATH_INCLUDED
#define INTMATH_INCLUDED
int gcd(int i, int j); 
int lcm(int i, int j);
#endif
```

**File `intmath.c`:**

```c
#include "intmath.h"

int gcd(int i, int j) {
    int temp;
    while (j != 0) {
        temp = i % j;
        i = j;
        j = temp;
    }
    return i;
}

int lcm(int i, int j) {
    return (i / gcd(i, j)) * j;
}
```

**File `testintmath.c`:**

```c
#include "intmath.h" 
#include <stdio.h>

int main(void) {
    int i, j;
    printf("Enter the first integer:\n");
    scanf ("%d", &i);
    printf("Enter the second integer: \n");
    scanf ("%d", &j);
    printf ("Greatest common divisor: %d.\n", gcd(i, j));
    printf ("Least common multiple: %d.\n", lcm(i, j));
    return 0;
}
```

**Dependencies in the example**

In this example, the dependencies are fairly straightforward:

* `intmath.c` depends on `intmath.h`, as it includes this header file to get the prototypes of `gcd` and `lcm` functions.
* `testintmath.c` also depends on `intmath.h`, as it uses the functions `gcd` and `lcm` which are declared in `intmath.h`. Furthermore, `testintmath.c` depends on `stdio.h` for the `printf` and `scanf` functions.



## Transitive Dependencies

#### Transitive Dependencies

Transitive dependencies describe the principle that if file A depends on B and B depends on C, then A depends on C. This can involve any number of intermediary steps.

To illustrate, let's use the files `intmath.h`, `intmath.c`, and `complexmath.h`, and `complexmath.c`.

1. **Single intermediary step (often referred to as indirect dependency):**

In the case of a single intermediary step, we have an example with `complexmath.c` and `intmath.h`.

**File `complexmath.h`:**

```c
#ifndef COMPLEXMATH_INCLUDED
#define COMPLEXMATH_INCLUDED
#include "intmath.h"
int calculate(int i, int j, int k);
#endif
```

In `complexmath.h`, it includes `intmath.h`. This means any .c file including `complexmath.h` will have a transitive dependency on `intmath.h`.

2. **Multiple intermediary steps:**

To demonstrate multiple intermediary steps, let's introduce another file, `advancedmath.h`.

**File `advancedmath.h`:**

```c
#ifndef ADVANCEDMATH_INCLUDED
#define ADVANCEDMATH_INCLUDED
#include "complexmath.h"
int advancedCalculate(int i, int j, int k, int l);
#endif
```

**File `advancedmath.c`:**

```c
#include "advancedmath.h"

int advancedCalculate(int i, int j, int k, int l) {
    return calculate(i, j, k) + l;
}
```

Here, `advancedmath.c` includes `advancedmath.h`, which in turn includes `complexmath.h`. Since `complexmath.h` includes `intmath.h`, `advancedmath.c` has a transitive dependency on `intmath.h` through multiple intermediary steps.

In both scenarios, the .c files depend on `intmath.h` and `intmath.c` through other header files, highlighting the concept of transitive dependencies.

## Cyclic Dependencies

Cyclic dependencies occur when two or more modules depend on each other, either directly or indirectly. These can make the code difficult to understand and maintain and are typically avoided where possible. However, for illustration, consider the following situation:

**File `intmath.h` (modified):**

```c
#ifndef INTMATH_INCLUDED
#define INTMATH_INCLUDED
#include "complexmath.h"
int gcd(int i, int j); 
int lcm(int i, int j);
#endif
```

Now `intmath.h` depends on `complexmath.h` (because it includes it), and `complexmath.h` depends on `intmath.h` (because it also includes it). This forms a cycle: `intmath.h` -> `complexmath.h` -> `intmath.h`. This is an example of a direct cyclic dependency. It's important to note that such situations are usually problematic (compilers can't handle such circular dependencies) and should be avoided in practice.





