# Background

Simply put, `make` is a program that enables programmers to combine the efficiency of compiling only what is necessary with the convenience of not having to manually track which parts of the codebase have changed.





Make is a dependency-tracking tool.&#x20;

## Motivation for Make

POINT IS SAVING OBJECT FILES.&#x20;

Suppose invoke GCC on a program consisting of three files--f1.c, f2.c, and f3.c:



Recall from Chapter 4 that GCC will _separately_ transform f1.c, f2.c, and f3.c into object files--f1.o, f2.o, and f3.o respectively--and then link the three object files--along with necessary library files--together to create an executable file--by default named a.out. This process is shown in Figure 1.

<figure><img src="../../.gitbook/assets/Group 104.png" alt="" width="563"><figcaption></figcaption></figure>

By default, GCC will discard the object files, leaving only the resulting executable.&#x20;





The purpose of this teqnique is to enable  teqnique is useful since it enables use to avoid redundant compilation.&#x20;





```c
/*--------------------------------------------------------------------*/
/* intmath.c                                                      */
/*--------------------------------------------------------------------*/

#include "intmath.h"

int gcd(int i, int j)
{
int temp;
while (j != 0) {
temp = i % j;
i = j;
j = temp;
}
return i;
}
int lcm(int i, int j)
{
return (i / gcd(i, j)) * j;
}
```

```c
/*--------------------------------------------------------------------*/
/* testintmath.c                                                      */
/*--------------------------------------------------------------------*/

#include <stdio.h>
#include "intmath.h"

int main(void)
{
int i, j;
printf("Enter the first integer:\n"); scanf("%d", &i);
printf("Enter the second integer:\n"); scanf("%d", &j);
printf("Greatest common divisor: %d.\n", gcd(i, j));
printf("Least common multiple: %d.\n", lcm(i, j));
return 0; 
}
```

```c
/*--------------------------------------------------------------------*/
/* intmath.h */
/*--------------------------------------------------------------------*/
#ifndef INTMATH_INCLUDED 
#define INTMATH_INCLUDED 
int gcd(int i, int j); 
int lcm(int i, int j); 
#endif
```

