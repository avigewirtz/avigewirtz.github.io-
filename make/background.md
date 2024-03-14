# Motivation For Make

Recall the testintmath program from precept 4, whose source code is shown below. We will use it as a running example throughout this chapter.&#x20;

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

For a small program like testintmath, rebuilding the entire thing every time a change is introduced is not a terrible approach, as it's a small program that doesn't take much time to build. But what if our program were much larger, say composed of 1000 .c files? First, having to type out all 1000 filenames whenever building our program would be exhausting. But that's not the real issue. After all, you could easily write a shell script to automate this process. The real issue is that rebuilding all 1000 source files would be extremely time-consuming and a drain on system resources. Surely there's a more efficient approach. And of course there is. It's called incremental or partial builds.&#x20;

## Incremental builds

Incremental builds is an approach where each build builds off the previous one. In other words, the first time you build a program you build the entire thing, but in subseqent build you only rebuild parts that have changed.

The strategy for employing incremental builds is in theory quite simple. We take advantage of the fact that a C program can be compiled as a bunch of independent units, and then linked together. You can think of this like a puzzle, where each piece can be constrcuted seperately, and then linked together to create a final product.&#x20;

In a C program, each .c file, along with the files included via header directives, comprises a translation unit. Each of these translation units can be translation to machine code, have the machine code version saved, and then linked together to form an executable. Then, if one translation unit changes, only that unit has to be recompiled, not the other ones.&#x20;

Let's show this in action for our testintmath program. This time we build in the manner shown in Figure 5. That is, we first invoke gcc217 with the -c option:

```
gcc217 -c testintmath.c intmath.c 
```

This preprocesses, compiles, and assembles intmath.c and testintmath.c, producing the object files intmath.o and testintmath.o. We then link intmath.o and testintmath.o, generating the testintmath executable:&#x20;

```
gcc intmath.c testintmath.c -o testintmath
```

Going forward, if we make a change to a file, we rebuild the .o files that are affected by the change, and then link all the .o files together to create the updated executable.&#x20;

<figure><img src="../.gitbook/assets/Group 28 (1).png" alt=""><figcaption><p>Figure 5.1: Dependency Graph for testintmath</p></figcaption></figure>

In our case, the dependency graph in Figure 2 makes it quite obvious what files have to be rebuilt after a change. We see that a change to testintmath.c affects testintmat.o and testintmath, but it does not affect intmath.o. Similarly, a change to intmath.c affects intmat.o and testintmath, but it does not affect testintmath.o. However, a change to intmath.o affects testintmath.o, intmath.o, and testintmath.&#x20;

<figure><img src="../.gitbook/assets/Group 64 (2).png" alt="" width="563"><figcaption></figcaption></figure>

#### Why Manual Incremental Builds are Difficult

As you can imagine, implementing incremental builds is tedious and error prone. Not only do you have top keep track of which files were changed since the last, you also have to keep track of which other files are affected by the changes. In our program, doing this is not fun, but it's also not incredibly dificult. But large-scale, real-world projects are far more complex, and have complex dependency chains. Doing all this work manualy is not only tedious, it's incredibly error-prone.&#x20;
