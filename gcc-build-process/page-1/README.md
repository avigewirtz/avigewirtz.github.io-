# Example Program

Let's now analyze each of the build stages in detail. To do so, we'll use the multi-file C program shown below as an example.&#x20;

{% tabs %}
{% tab title="testcircle.c" %}
{% code lineNumbers="true" %}
```c
/*--------------------------------------------------------------*/
/* testcircle.c - calculates area of a circle given its radius. */
/*--------------------------------------------------------------*/
 
#include <stdio.h>
#include <stdlib.h> 
#include "circle.h" 
   
int main(void) {

  double radius, area;
 
  radius = 12.7;
  area = circleArea(radius);
  
  printf("Area of circle with radius %.2f is %.2f\n", radius, area);

  return EXIT_SUCCESS;
}
```
{% endcode %}
{% endtab %}

{% tab title="circle.c" %}
{% code lineNumbers="true" %}
```c
/*---------------------------------------------------------------*/
/* circle.c                                                      */
/*---------------------------------------------------------------*/

#include "circle.h"
#define PI 3.14159

double circleArea(double radius) {
    return PI * radius * radius;
}
```
{% endcode %}
{% endtab %}

{% tab title="circle.h" %}
{% code lineNumbers="true" %}
```c
#ifndef CIRCLE_H
#define CIRCLE_H

double circleArea(double radius);

#endif
```
{% endcode %}
{% endtab %}
{% endtabs %}



We'll build our program using the `--save-temps` option:

```
gcc217 --save-temps intmath.c testintmath.c -o testintmath
```



```
ls

```
