# gcc extra

##

## Building a single-file C program

Consider the circle.c program shown below. It will serve as a running example throughout this chapter.&#x20;

{% code lineNumbers="true" %}
```c
/*-----------------------------------------------------*/
/* circle.c                                        */
/*                                                     */
/* Calculates the area of a circle given its radius.   */
/*-----------------------------------------------------*/
 
#include <stdio.h>
#include <stdlib.h> 
#define PI 3.14159

double calculateArea(double radius) {
    return PI * radius * radius;
}

/* Prompts user for radius of circle. Returns 
   EXIT_FAILURE if input is invalid. Otherwise, prints 
   circle's area to stdout and returns 0. */  
   
int main(void) {

  double radius, area; 

  printf("Enter radius of circle: ");
  if (scanf("%lf", &radius) != 1 || radius <= 0) {
    printf("Invalid input. Must be a positive number.\n");
    exit(EXIT_FAILURE);
  }

  area = calculateArea(radius);

  printf("The area of the circle is: %.2f\n", area);

  return 0;
}

```
{% endcode %}

To build circlearea. c, we can invoke:

```
gcc217 circle.c
```

The result will be an executable file named a.out. We can customize the output name of the file by using the -o option:&#x20;

```
gcc circle.c -o circl
```

This tells gcc to name the executable circle, rather than a.out. We can run the executable by invoking it like so:

```
./circle
```

### Building a multi-file C program

A C program can be split up into multiple files.  This makes programs easier to maintain, especially as they grow larger. Suppose we want to split up circle.c into two files: circle.c and testcircle.c. circle.c will contain the calculateArea function, while testcirclearea.c will contain the main function, serving as a client of circlearea.c. Unfortunately, splitting our program in this manner is not as simple as creating a new file named testcircle.c and pasting the main function into it. If we were to attempt this and try to build our program, we would get the following error:



{% tabs %}
{% tab title="testcircle.c" %}
{% code lineNumbers="true" %}
```c
/*-----------------------------------------------------*/
/* testcircle.c                                        */
/*                                                     */
/* Calculates the area of a circle given its radius.   */
/*-----------------------------------------------------*/
 
#include <stdio.h>
#include <stdlib.h> 

/* Prompts user for radius of circle. Returns 
   EXIT_FAILURE if input is invalid. Otherwise, prints 
   circle's area to stdout and returns 0. */  
   
int main(void) {

  double radius, area; 

  printf("Enter radius of circle: ");
  if (scanf("%lf", &radius) != 1 || radius <= 0) {
    printf("Invalid input. Must be a positive number.\n");
    exit(EXIT_FAILURE);
  }

  area = calculateArea(radius);

  printf("The area of the circle is: %.2f\n", area);

  return 0;
}

```
{% endcode %}
{% endtab %}

{% tab title="circle.c" %}
{% code lineNumbers="true" %}
```c
/*-----------------------------------------------------*/
/* circle.c                                            */
/*-----------------------------------------------------*/

#define PI 3.14159

/* calculates the area of a circle given its radius */
double calculateArea(double radius) {
    return PI * radius * radius;
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

To build our program, we can invoke the following command:



{% tabs %}
{% tab title="testcircle.c" %}
```c
/*-----------------------------------------------------*/
/* testcircle.c                                        */
/*                                                     */
/* Calculates the area of a circle given its radius.   */
/*-----------------------------------------------------*/
 
#include <stdio.h>
#include <stdlib.h> 
#include "circle.h" 

/* Prompts user for radius of circle. Returns 
   EXIT_FAILURE if input is invalid. Otherwise, prints 
   circle's area to stdout and returns 0. */  
   
int main(void) {

  double radius, area; 

  printf("Enter radius of circle: ");
  if (scanf("%lf", &radius) != 1 || radius <= 0) {
    printf("Invalid input. Must be a positive number.\n");
    exit(EXIT_FAILURE);
  }

  area = calculateArea(radius);

  printf("The area of the circle is: %.2f\n", area);

  return 0;
}

```
{% endtab %}

{% tab title="circle.c" %}
```c
/*-----------------------------------------------------*/
/* circle.c                                            */
/*-----------------------------------------------------*/

#include "circle.h"
#define PI 3.14159

/* calculates the area of a circle given its radius */
double calculateArea(double radius) {
    return PI * radius * radius;
}
```
{% endtab %}

{% tab title="circle.h" %}
```c
#ifndef CIRCLE_H
#define CIRCLE_H

double calculateArea(double radius);

#endif
```
{% endtab %}
{% endtabs %}

To build our program, we can invoke the following command:

