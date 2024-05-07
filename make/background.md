# Introduction

In a nutshell, make is a software tool that automates the process of incremental builds. The key to understanding make is understanding what incremental builds are and how to implement them manually. Once you grasp this, the mechanics and role of make become clear.

{% hint style="warning" %}
Before reading this chapter, ensure you're familiar with the GCC build process. An overview is provided in [GCC Build Process](broken-reference/).
{% endhint %}

## **Incremental Builds**

Incremental builds optimize the build process by recompiling only the code modules that have changed since the last build, instead of the entire project. This significantly reduces build times, especially in larger projects. We'll start with a mathematical example to illustrate the core concept, then translate that to the world of C programming

#### Mathematical Example

Consider the following mathematical functions:

$$A = B + C$$

$$B = (X + H)^2$$

$$C = (Y + H)^2$$

Given the values $$X=3, \ Y=4,\ H=2$$, the process to compute $$A$$ involves the following computations:

* $$B =  (3 + 2)^2 = 25$$
* $$C = (4 + 2)^2 = 36$$
* $$A = 25 + 36 = 61$$

Now, let's say we change $$X$$ to $$5$$ but keep $$Y$$ and $$H$$ the same. Since $$C$$ does not depend on $$X$$, we can recompute $$A$$ without recomputing $$C$$:

* $$B = (5 + 2)^2 = 49$$
* $$A = 49 + 36 = 80$$

Now, if we were to change the value $$H$$, recomputing $$A$$ we require us to first recompute both $$B$$ and $$C$$, since both of them depend on $$H$$.&#x20;

#### Dependency Graph

We can formally describe the dependencies among the A, B, C, X, Y, and H using a dependency graph (Figure 14).&#x20;

<figure><img src="../.gitbook/assets/Frame 26.png" alt="" width="375"><figcaption><p>Dependency Graph</p></figcaption></figure>

In this graph, a _directed edge_ A -> B indicates that A directly depends on B, meaning that a change to B requires A to be updated. If A -> B and B -> C, then A is indirectly (or transitively) dependent on C. With this dependency graph, determining how to recompute A after a change to X, Y, or H is extremely simple:

* **If X changes:** We recompute B and then A.&#x20;
* **If Y changes:** We recompute C and then A.&#x20;
* **If H changes:** We recompute B and C (in any order) and then recompute A.

#### Transition to C

The core principles  we just described apply directly to C programs. Let's demonstarte with a practical example. Consider the `testintmath` program from precept 4, whose source code is shown below.

{% tabs %}
{% tab title="testintmath.c (client)" %}
{% code lineNumbers="true" %}
```c
#include "intmath.h"
#include <stdio.h>

int main() {
  int i, j;
  printf("Enter the first integer:\n");
  scanf("%d", &i);
  printf("Enter the second integer:\n");
  scanf("%d", &j);
  printf("Greatest common divisor: %d.\n", gcd(i, j));
  printf("Least common multiple: %d.\n", lcm(i, j));
  return 0;
}
```
{% endcode %}
{% endtab %}

{% tab title="intmath.c (implementation)" %}
{% code lineNumbers="true" %}
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
{% endcode %}
{% endtab %}

{% tab title="intmath.h (interface)" %}
{% code lineNumbers="true" %}
```c
#ifndef INTMATH_INCLUDED
#define INTMATH_INCLUDED

int gcd(int i, int j);
int lcm(int i, int j);

#endif
```
{% endcode %}
{% endtab %}
{% endtabs %}

Explain dependencies

$$\text{testintmath} = \text{link}(\text{testintmath.o, intmath.o})$$

$$\text{testintmath.o} = \text{compile}(\text{testintmath.c, intmath.h})$$

$$\text{intmath.o} = \text{compile}(\text{intmath.c, intmath.h})$$

<figure><img src="../.gitbook/assets/Group 125 (1).png" alt="" width="563"><figcaption><p>Figure 12.3: testintmath's dependency graph</p></figcaption></figure>

{% hint style="info" %}
Recall that the contents of #included files are inserted by the preprocessor before compilation proper begins. Hence, object files are derived from their corresponding C file as well as all #included source files.&#x20;
{% endhint %}

The dependency graph is shown in Figure&#x20;

#### Building `testintmath`

When we build `testintmath` for the first time, all object files and the execvutable have to be built. We can do so as follows:

1. Build `intmath.o`. This is done by invoking `gcc217` with the `-c` option on `intmath.c`:

```
gcc217 -c intmath.c
```

2. Build `testintmath.o`:

```
gcc217 -c testintmath.c
```

3. Build `testintmath`. This is done by linking `intmath.o` and `testintmath.o`:

```
gcc217 intmath.o testintmath.o -o testintmath
```

{% hint style="info" %}
Note that we could have built both `testintmath.o` and `intmath.o` in a single command (e.g., `gcc217 -c testintmath.c intmath.c`). The underlying GCC operations would have been the same.&#x20;
{% endhint %}

#### Rebuilding `testintmath`

* **If `intmath.c` is modified:** We rebuild `intmath.o` and then `testintmath`:&#x20;

```bash
gcc217 -c intmath.c
gcc217 intmath.o tetsintmath.o -o testintmath
```

* **If `testintmath.c` is modified:** We rebuild `testintmath.o` and then `testintmath`.&#x20;

```
gcc217 -c testintmath.c
gcc217 intmath.o tetsintmath.o -o testintmath
```

* **If `intmath.h` is modified: H changes:** We rebuild `intmath.o` and `testintmath.o` (in any order) and then `testintmath`:

```
gcc217 -c intmath.c
gcc217 -c testintmath.c
gcc217 intmath.o tetsintmath.o -o testintmath
```

{% hint style="info" %}
As we saw in [GCC Build Process](broken-reference/), GCC always builds C programs in four sequential stages: preprocessing, compilation, assembly, and linking. This is the case whether we build a via a single command (e.g., `gcc217 foo.c bar.c -o foobar`), or via two commands (e.g., `gcc217 -c foo.c bar.c` followed by `gcc217 foo.o bar.o -o foobar`). Fundamentally, the only difference between these two build approaches is that the two-command approach retains the intermediate object files while the single-command approach does not.

When I distinguish between "single-step" and "two-step" build approaches, I'm referring to how we might conceptualize the build process, not the underlying GCC operations.&#x20;
{% endhint %}
