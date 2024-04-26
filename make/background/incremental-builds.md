# Incremental Builds

Incremental builds is an approach where each build builds off the previous one. The first time you build a program, you compile all of its source files. In subsequent builds, however, you compile only the source files that have changed since the last build or were affected by changes.

They key to implementing incremental builds is to always build a program in two steps. In the first step, you compile the source files into object files. This is done by invoking `gcc217` with the `-c` option. The key is that you only compile those source files that would produce object files different from those generated in the previous build. In the second step, you link all the object files (i.e., the "new" and "old" object files) together to produce the executable.

## Dependency graphs

To know which files need to be rebuilt after changes to the source code, you need to have a good grasp of the program's dependencies. An efficient method of doing so is via a dependency graph, like the one shown in Figure 2.3.&#x20;

<figure><img src="../../.gitbook/assets/Group 132.png" alt=""><figcaption></figcaption></figure>

In this graph, each node represents a file.

## Example

To demonstrate incremental builds, we'll use the `testintmath` program from precept 4, whose source code is shown below.&#x20;

{% tabs %}
{% tab title="testintmath.c (client)" %}
{% code lineNumbers="true" %}
```c
#include "intmath.h"
#include <stdio.h>

int main() {
  int i, j;
  printf("Enter the first integer:\n");
  scanf("%sd", &i);
  printf("Enter the second integer:\n");
  scanf("%sd", &j);
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

The first time we build `testintmath`, we invoke gcc with the `-c` option on `intmath.c` and `testintmath.c`:

```
gcc217 -c intmath.c testintmath.c 
```

This compiles `intmath.c` and `testintmath.c` into object files `intmath.o` and `testintmath.o`. We then we invoke gcc on `intmath.o` and `testintmath.o`:

```
gcc217 intmath.o testintmath.o -o testintmath
```

This links the object files together, generating the executable `testintmath`. This process is summarized in Figure 7.2.&#x20;

<figure><img src="../../.gitbook/assets/Group 147 (2).png" alt="" width="563"><figcaption></figcaption></figure>

Going forward, if we modify a source file, we only need to rebuild the affected `.o` files, and then link the all the `.o` files together to produce the updated executable. For example, suppose we modify `intmath.c`. To rebuild our program, we invoke `gcc217 -c` on `intmath.c` alone:

```
gcc217 -c intmath.c
```

We then link `intmath.o` (the "new" object file) with `testintmath.o` (the "old" object file) to produce the updated executable:

```
gcc217 tesintmath.o intmath.o -o testintmath
```

If we were to modify `intmath.h`, the results would be more dramatic. Because `testintmath.c` and `intmath.c` both #include `intmath.h`, `testintmath.o` and `intmath.o` would both be affected by a change in `intmath.h`. Thus, we'd have to recompile and link the entire program.&#x20;
