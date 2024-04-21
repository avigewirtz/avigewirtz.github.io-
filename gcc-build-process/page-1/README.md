# Example Program

Now that we understand the four stages involved in building a C program, let's see them in action with a practical example. Consider the multi-file C program shown below. It will serve as a running example throughout this chapter, allowing us to demonstrate how the GCC build process works. To build our program, we invoke the following command:

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
