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

We can build our program by invoking:

```
gcc217 testintmath.c intmath.c -o testintmath
```

Now suppose after building testintmath, we make a change to one of the source files, say intmath.c. To incorporate the change, we of course need to rebuild testintmath. We can do so by invoking the same command we previously invoked:

```
gcc217 testintmath.c intmath.c -o testintmath
```

For a small program like testintmath, rebuilding all source files whenever a change is introduced is not a terrible approach, since it's a small program and building it doesn't take much time. But what if our program were much larger, say composed of 1000 .c files? Rebuilding all 1000 source files would be extremely time-consuming and a drain on system resources. Surely there's a more efficient approach. And of course there is. It's called incremental or partial builds.&#x20;

## Incremental builds

Incremental builds is an approach where each build builds off the previous one. In other words, the first time you build a program you build the entire thing, but in subsequent build you only rebuild parts that have changed.

The strategy for employing incremental builds is in theory straightforward. Recall that gcc build's C programs in four sequential stages: preprocessing, compilation, assembly, and linking. This process is shown in Figure 5.2. By default, the intermediate files are not retained.&#x20;

<figure><img src="../.gitbook/assets/Group 118.png" alt="" width="375"><figcaption></figcaption></figure>

We don't care about .i or .s files, but the key to implementing incremental builds is saving the .o files. The object files are a machine code version of the program, but stored in two independent units. testintmath.o is derived from testintmath.c and intmath.h, but is completely independent of intmath.c. Similarly, intmath.c is completely independent of testintmath.c. Thus a change to testintmath.c has no bearing on intmath.o, and a change to intmath.c has no bearing on testintmath.o. However, a change to will not affect either .c file will not affect the other .c file's corresponding  testintmath.o is a machine code version of testintmath.c and intmath.h, and intmath.o is a machine code version of This way, if a subsequent change to the source code does not affect a .o file, it can be reused.  Let's now build testintmath again, but this time ensuring to save to object files. To do so, we invoke gcc twice. First we invoke it with the -c option, which tells gcc to stop the build process after assembly, and save the output in object files.&#x20;

```
gcc217 -c intmath.c testintmath.c 
```

Then we invoke gcc on the .o files, which links them together, generating the executable testintmath:

```
gcc217 intmath.o testintmath.o -o testintmath
```

Going forward, if we make a change to a file, we rebuild the .o files that are affected by the change, and then link all the .o files together to create the updated executable.&#x20;

<figure><img src="../.gitbook/assets/Group 28 (1).png" alt=""><figcaption><p>Figure 5.1: Dependency Graph for testintmath</p></figcaption></figure>

In our case, the dependency graph in Figure 2 makes it quite obvious what files have to be rebuilt after a change. We see that a change to testintmath.c affects testintmat.o and testintmath, but it does not affect intmath.o. Similarly, a change to intmath.c affects intmat.o and testintmath, but it does not affect testintmath.o. However, a change to intmath.o affects testintmath.o, intmath.o, and testintmath.&#x20;

<figure><img src="../.gitbook/assets/Group 64 (2).png" alt="" width="563"><figcaption></figcaption></figure>

#### Why Manual Incremental Builds are Difficult

As you can imagine, implementing incremental builds is tedious and error prone. Not only do you have top keep track of which files were changed since the last, you also have to keep track of which other files are affected by the changes. In our program, doing this is not fun, but it's also not incredibly dificult. But large-scale, real-world projects are far more complex, and have complex dependency chains. Doing all this work manualy is not only tedious, it's incredibly error-prone.&#x20;











Incremental builds relies on understanding dependencies between files to determine which need recompilation after a change.
