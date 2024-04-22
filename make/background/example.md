# Example

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



First, we build a dependency graph.&#x20;

<figure><img src="../../.gitbook/assets/Group 117.png" alt="" width="563"><figcaption></figcaption></figure>

The first time we build testintmath, we invoke gcc with the -c option on both intmath.c and testintmath.c:

```
gcc217 -c intmath.c testintmath.c 
```

Then we invoke gcc on the .o files, which links them together, generating the executable testintmath:

```
gcc217 intmath.o testintmath.o -o testintmath
```

Going forward, if we make a change to a file, we only need to rebuild the .o files that are affected by the change, and then link the updated .o files with the "old" .o files to create the updated executable. Figure 5-1 summarizes the commands we invoke after a change to each file.&#x20;



<figure><img src="../../.gitbook/assets/Group 64 (2).png" alt="" width="563"><figcaption></figcaption></figure>

d
