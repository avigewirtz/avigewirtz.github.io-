# Page 1

The process of transforming one or more C source files into an executable file can be logically divided into three main phases:

* Preprocessing phase. Textual substitutions.&#x20;
* Translation phase. C code is converted to machine code. GCC performs translation in two stages. First translates to assembly and then from assembly to machine code.&#x20;
* Linking phase.&#x20;

Tranlsation phase is generally understood. We'll demonstrate reason for preprocessor and linker using the following program.&#x20;

{% code lineNumbers="true" %}
```c
/*--------------------------------------------------------------------*/
/* circle.c                                                           */
/*                                                                    */
/* Calculates the area of a circle given its radius.                  */
/*--------------------------------------------------------------------*/
 
int printf(const char *format, ...);
int scanf(const char *format, ...);
void exit(int status); 
 
double calculateArea(double radius) {
    return 3.14159 * radius * radius;
}
  
/* Prompts user for the radius of a circle. Returns
   EXIT_FAILURE if input is invalid. Otherwise, prints
   circle's area to stdout and returns 0. */  
int main(void) {

  double radius, area;

  printf("Enter radius of circle: ");
  if (scanf("%lf", &radius) != 1 || radius <= 0) {
    /* For simplicity, printing to stdout instead of stderr. */
    printf("Invalid input. Must be a positive number.\n");
    exit(1);
  }

  area = calculateArea(radius);

  printf("The area of the circle is: %.2f\n", area);

  return 0;
}
```
{% endcode %}

Program makes calls to three library functions--printf, scanf, and exit. Definitions not in our file. Some compiler recognize calls to the standard functions and to generate the appropriate code directly. Pascal, which provides a small set of standard functions, takes this approach, but it is not feasible for C, because of the large number of standard functions defined by the C standard. It would add significant complexity to the compiler and would require a new compiler version each time a function was added, deleted, or modified.Two questions to consider. 1. How is the library code inserted? When is it inserted?&#x20;



At some point in the build process, the definitions for these functions must be inserted into the code. Consider a couple of approaches.&#x20;
