# Motivation For Make

Recall the testintmath program from precept 4, whose source code is shown below.&#x20;

{% tabs %}
{% tab title="testintmath.c" %}
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

{% tab title="intmath.c" %}
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

{% tab title="intmath.h" %}
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

We can build our program by invoking the following command:

```
gcc217 testintmath.c intmath.c -o testintmath
```

Now suppose after building our testintmath, we decide to make a change one of the source files, say intmath.c. To incorporate the change, we of course of have to rebuild testintmath. We can do so by invoking the same command we previously invoked:

```
gcc217 testintmath.c intmath.c -o testintmath
```

For a small program like testintmath, rebuilding the entire thing every time a change is introduced is not a terrible approach, as it's a small program that doesn't take much time to build. But what if our program were composed of, say, 1000 source files? First, having to type out all 1000 filenames whenever building our program would be exhausting. But that's not the real issue. After all, you could easily write a shell script to automate this process. The real issue is that rebuilding all 1000 source files would be extremely time-consuming and a drain on system resources. Surely there's a more efficient approach. And of course there is. It's called incremental or partial builds.&#x20;

## Incremental builds

Incremental builds is an appraoch where each build builds off the previous one. In other words, the first time you build a program you build the entire thing, but in subseqent build you only rebuild parts that have changed.

The strategy for employing incremental builds is in theory quite simple. We take advantage of the fact that a C program can be compiled as a bunch of independent units, and then linked together. You can think of this like a puzzle, where each piece can be constrcuted seperately, and then linked togethetr to create a final prodyct.&#x20;

In a C program, each .c file, along with the files included via header directives, comprises a translation unit. Each of these translation units can be translation to machine code, have the machine code version saved, and then linked together to form an executable. Then, if one translation unit changes, only that unit has to be recompiled, not the other ones.&#x20;

Let's show this in action for our testintmath program. This time we build it by first invoking gcc with the -c option:

```
gcc217 -c testintmath.c intmath.c 
```

This preprocesses, compiled, and assembled each file, and stops there, saving the output in testintmath.o and intmath.o. We then link these two object files together to generate the executable testintmath:

```
gcc217 testintmath.o intmath.o -o testintmath
```





```bash
gcc -c intmath.c testintmath.c
```

This preprocesses, compiles, and assembles intmath.c and testintmath.c, producing the object files intmath.o and testintmath.o. Note that in the preprocessing stage of both intmath.c and testintmath.c, the contents are intmath.h were inserted into each.  Thus, `intmath.o` is derived from both `intmath.c` and `intmath.h`. Similarly, testintmath.o is derived from both `intmath.c` and `intmath.h`.



We then link intmath.o and testintmath.o, generating the testintmath executable:&#x20;

```
gcc intmath.c testintmath.c -o testintmath
```



<figure><img src="../.gitbook/assets/Group 28 (1).png" alt=""><figcaption></figcaption></figure>



### Rebuilding testintmath

Now imagine we make a change to one of our source files. Our goal is to rebuild testintmath by recompiling the minimum necessary source files. An easy way to figure our what changes require which files to be rebuilt is via a dependency graph.&#x20;











&#x20; recompile the mininum  To rebuild testintmath, we need only recompile intmath.c

\<over here i want to explain how if we make changes we can use partial builds to rebuild testintmath. i want to explain using a dependency graph of testintmath, where each node represents a file, and directed edges (arrows) between these nodes indicate a dependency, where an edge from file A to file B signifies that B is dependent on A. In other words, a change in file A requires file B to be updated.>









<figure><img src="../.gitbook/assets/Group 28 (1).png" alt=""><figcaption></figcaption></figure>





our objective is to generate a new executable by recompiling the minimum necessary files. To do this accurately, we need to have a thorough understanding of the program's dependencies, which can be visualized using a dependency graph.

In such a graph, each node represents a file, and directed edges (arrows) between these nodes indicate a dependency, where an edge from file A to file B signifies that B is dependent on A. In other words, a change in file A requires file B to be updated. A dependency graph for testintmath is shown in Figure 2.&#x20;

&#x20;

<figure><img src="../.gitbook/assets/Group 41.png" alt=""><figcaption></figcaption></figure>



<figure><img src="../.gitbook/assets/Group 39.png" alt=""><figcaption></figcaption></figure>
