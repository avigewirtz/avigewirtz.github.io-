# Dependencies

In our earlier discussion on code reusability, we explained how certain files can be dependent on others for proper execution. For instance, a simple C program, `hello.c`, might depend on the printf library function, and thus, the `stdio.h` header file.

If either the `stdio.h` file or the library function file changes in a way that alters their interfaces, all files that use them can potentially break.

Let's consider an example where the prototype for the `printf` function in the `stdio.h` file is changed from `int printf(const char *format, ...);` to `int printf(int num, const char *format, ...);`. This would break all programs that use `printf` since they would now need to provide an additional integer argument at the beginning.

Will will consider 4 types of dependencies: direct dependencies, indirect dependencies, transitive dependencies, cyclic dependencies.&#x20;

## Direct Dependencies

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
cCopy code#include "intmath.h"

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
cCopy code#include "intmath.h" 
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

## **Indirect Dependencies**

For an example of indirect dependencies, let's create a new file, `complexmath.h`, which uses the functions from `intmath.h`.

**File `complexmath.h`:**

```c
cCopy code#ifndef COMPLEXMATH_INCLUDED
#define COMPLEXMATH_INCLUDED
#include "intmath.h"
int calculate(int i, int j, int k);
#endif
```

Here, `complexmath.h` indirectly depends on `intmath.h` because it uses the functions declared in `intmath.h`.

## Transitive Dependencies

Transitive dependencies are a property of indirect dependencies. If file A depends on B and B depends on C, then A depends on C. This is demonstrated in our new file:

**File `complexmath.c`:**

```c
cCopy code#include "complexmath.h"

int calculate(int i, int j, int k) {
    return lcm(i, gcd(j, k));
}
```

Here, `complexmath.c` has a transitive dependency on `intmath.h` and `intmath.c` through `complexmath.h`. This is because it uses the `lcm` and `gcd` functions, which are defined in `intmath.c` and declared in `intmath.h`.

## Cyclic Dependencies

Cyclic dependencies occur when two or more modules depend on each other, either directly or indirectly. These can make the code difficult to understand and maintain and are typically avoided where possible. However, for illustration, consider the following situation:

**File `intmath.h` (modified):**

```c
cCopy code#ifndef INTMATH_INCLUDED
#define INTMATH_INCLUDED
#include "complexmath.h"
int gcd(int i, int j); 
int lcm(int i, int j);
#endif
```

Now `intmath.h` depends on `complexmath.h` (because it includes it), and `complexmath.h` depends on `intmath.h` (because it also includes it). This forms a cycle: `intmath.h` -> `complexmath.h` -> `intmath.h`. This is an example of a direct cyclic dependency. It's important to note that such situations are usually problematic (compilers can't handle such circular dependencies) and should be avoided in practice.





