# Introduction

make is a software tool that automates incremental builds. The key to understanding make is understanding what incremental builds are. Once you understand this, the mechanics and role of make become obvious.&#x20;

{% hint style="warning" %}
Note: Before reviewing this chapter, ensure you're familiar with the GCC build process. An in depth overview is provided in [GCC Build Process](broken-reference).
{% endhint %}

## Incremental builds

Incremental builds is an approach where each build builds off the previous one. The first time you build a program you build the entire thing, but in subsequent build you only rebuild parts that have been affected by changes.

They key to implementing incremental builds we always treat building as a two step process. In the first step, each of the files is translated into object code. In the second step, each of the .o files is linked to produce the executable.&#x20;

## Understanding dependencies in a C program

Implementing incremental builds requires a good understanding of the project's dependencies. Easiest way to understand dependencies is via a dependency graph. Constructing a dependency graph is quite straightforward:

1. Create a node for each .c and .h file:&#x20;

<figure><img src="../.gitbook/assets/Group 92.png" alt=""><figcaption></figcaption></figure>

2. Create a corresponding .o node for each .c file, and draw an arrow from each .c file to its corresponding .o file:&#x20;

<figure><img src="../.gitbook/assets/Group 102 (2).png" alt=""><figcaption></figcaption></figure>

2. For each .h file, if it's included in a .c file, drar an arrow from the .h file to the same .o file that the .c file points to. For example, if x.h is #included in a.c and b.c, draw an arrow from x.h to a.o and b.o:

<figure><img src="../.gitbook/assets/Group 99.png" alt=""><figcaption></figcaption></figure>

4. Create a node for the executable, and draw an arrow from each .o node to the executable:&#x20;

<figure><img src="../.gitbook/assets/Group 100.png" alt=""><figcaption></figcaption></figure>

5. For extra clarity, it's helpful to also include the commands to generate each file:

<figure><img src="../.gitbook/assets/Group 111 (1).png" alt=""><figcaption></figcaption></figure>

In this graph, an arrow from file A to file B indicates that file B depends on A. Meaning, if A is modified, B has to be rebuilt.&#x20;

* Two levels of dependencies
* direct dependencies
* Indirect dependencies

## Example

Recall the testintmath program from precept 4, whose source code is shown below. We will use it as a running example throughout this chapter.&#x20;

{% tabs %}
{% tab title="testintmath.c (client)" %}
{% code lineNumbers="true" %}
```c
/********************************************************************/
/* tesintmath.c                                                     */
/* This program calculates the greatest common divisor (GCD) and    */
/* least common multiple (LCM) of two user-entered integers.        */
/********************************************************************/

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



## Incremental builds



```
gcc217 -c intmath.c testintmath.c 
```

Then we invoke gcc on the .o files, which links them together, generating the executable testintmath:

```
gcc217 intmath.o testintmath.o -o testintmath
```

Going forward, if we make a change to a file, we only need to rebuild the .o files that are affected by the change, and then link the updated .o files with the "old" .o files to create the updated executable.&#x20;

For example, suppose we change intmath.c. To rebuild tesintmath, we invoke gcc with the -c option on intmath.c alone:

```
gcc217 -c intmath.c 
```





<figure><img src="../.gitbook/assets/Group 64 (2).png" alt="" width="563"><figcaption></figcaption></figure>

#### Why Manual Incremental Builds are Difficult

As you can imagine, implementing incremental builds is tedious and error prone. Not only do you have top keep track of which files were changed since the last, you also have to keep track of which other files are affected by the changes. In our program, doing this is not fun, but it's also not incredibly dificult. But large-scale, real-world projects are far more complex, and have complex dependency chains. Doing all this work manualy is not only tedious, it's incredibly error-prone.&#x20;











Incremental builds relies on understanding dependencies between files to determine which need recompilation after a change.
