# working

* before we discuss the four stage compilation process, let’s first discuss a compilation technique known as separate compilation. This means that it compiled a each file seperately and only merges the content after. Suppose a program consists of two files: f1.c and f2.c. GCC converts each to machine code and then merges the contents to create an executable.&#x20;

<figure><img src="../.gitbook/assets/Group 16.png" alt="" width="149"><figcaption></figcaption></figure>

To understand why this is advantageous, let’s consider a simple C program with two source files: `main.c` and `circle.c`.

* Suppose we have a C program whose source code is distributed among two files: main.c and circle.c. Main.c contained the main method, which calls the area function in circle.c, which cacluvates the area of a circle based on its circumfrence. The entire source code for main.c and circle.c is not important. The relevant parts for our purposes are shown below.

{% code title="main.c" %}
```c
...
...
...
int main() {
    double area = calculateArea(10);
    return 0;
}
...
...
...
```
{% endcode %}

{% code title="circle.c" %}
```c
...
...
...
double calculateArea(double circumference) {
    double radius = circumference / (2 * 3.14159);
    return 3.14159 * radius * radius;
}
...
...
...
```
{% endcode %}

* To generate an executable, we pass both files to gcc as input, and it generates a single executable file.&#x20;
* Because the executable is generated from both main.c and squared.c, it goes without saying that at some point, the compiler had to have merged their contents together.&#x20;





The merging of `main.c` and `circle.c` by GCC can be conceptualized in two ways:



1. **Merging Before Compilation**
2. **Merging After Compilation**

* When does GCC merge their contents? There are two ways we can envision how GCC merges their contents. The first approach, would be to merge the contents of main.c and squared.c together before compilation begins. In other words, to merge their source code and compile it as a single unit.&#x20;
* This approach is inefficient, however, since if the contents of either main.c or squared.c is modified, both files have to be recompiled.&#x20;
* An alternative, much more efficient approach is for the compiler to compile main.c and squared.c separately into object files. These files are not executable since main and external reference. and give the user the option to save these versions. To generate an executable, the compiler will link the
