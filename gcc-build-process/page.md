# Page











Consider the circle.c program shown below. We'll use it as a running example throughout this chapter. Notice that this program does not use any preprocessor directives, and it does not use any library functions. It is essentially a self-contained program.&#x20;

{% code title="circle.c" lineNumbers="true" %}
```c
double calculateArea(double radius) {
    return 3.14159 * radius * radius;
}
  
int main() {

  double radius = 6.2, area;

  area = calculateArea(radius);

  return 0;
}
```
{% endcode %}

In a perfect world, we'd be able to load this program into memory and is and run it. Unfortunately, however, no modern computer understands C code. Each CPU has a unique set of instructions it can execute, known as machine code. While there's no universal standard for machine code, as each manufacturer designs its own for their specific device, two basic characteristics of machine code are consistent across all modern computers.

First, machine code is a binary language, consisting entirely of 1s and 0s. While there's no inherent requirement for machine code to use a binary system (historically, some computers used decimal systems), binary has proven to be the most efficient, leading to its adoption in all modern computers. Second, instructions in machine code are very basic, rarely exceeding the complexity of adding two numbers or transferring data between memory locations.
