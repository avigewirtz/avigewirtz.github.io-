# Linker and Preprocessor

## The linker

Suppose we have a C program spread across 100 source files. This might seem like a lot, but many real-world applications have far more. One of these files contains the `main` function, the entry point of the program. This file calls functions defined in other files, which in turn use functions defined in additional files. Our program also uses functions in the C standard library. Our goal is to transform this collection of source files into a single executable file that can be loaded into memory and run.

Consider different approaches C compiler designers might use to build this program. One approach would be for the compiler to first combine all source files and the relevant C standard library code into a single, monolithic unit, and then translate that unit into machine code. The resulting file would be a single, cohesive unit, that can be loaded into memory as is and executed. Tis method would admittedyl present some challenges relating to implementing scoping and the like, but we can devise clever slutions for these.

The main problem with this approach is that the _entire_ program must be recompiled whenever _any_ change is made, no matter how small. This would be incredibly time-consuming and inefficient, especially for large projects.

The approach C compilers use is to first compile each source file separately into its own machine code file, known as a **relocatable object file**. A separate program called the **linker** then combines all the relocatable object files, including those from the C standard library, to generate a final, **executable object file**.&#x20;

#### Challenges of separate compilation

* addresses. solution is assembler leaves them blank for the linker to fill in.&#x20;
* type checking.  In separate compilation scheme, compiler only processes one file at a time. So, say we have a program composed of two files, foo.c and bar.c. When the compiler is processing foo.c, it has no knowledge of the contents of bar.c, that we plan on using it together with foo.c, or even that bar.c exists at all. It only looks at foo.c. Consider the following scenario:

{% code title="foo.c" %}
```c
int main() {
    bar(int 1, double 2);
    return 0;
}
```
{% endcode %}

Here, `foo.c` calls the `bar` function, defined in bar.c. The problem, however, is that when compiling foo.c, the compiler doesn't have a clue what the function bar is. It doesn't know it's return type, not does it know that it in fact takes two arguments--an int and a double. The compiler can led it slide, as is was the case in C80/C90, where it assumed the function was called correctly and returned an int. This has proven to be extremely errorn prone, however, which is why C99 prohibs calling a function in this manner. &#x20;

The solution is that we insert prototype of all functions called at the top of the file. When the compiler processes foo.c, this is what it sees:

{% code title="foo.c" %}
```c
void bar(int i, double j);

int main() {
    bar(int 1, double 2);
    return 0;
}
```
{% endcode %}

The prototype is essentially our way of telling the compiler that we have a funtion named bar that takes an int and double as arguments and returns nothing. Now, when we make the call, the compiler can type check.&#x20;

In fact, even if the function we're calling is from the C Standard Library, we also have to declare it first.&#x20;

### Header Files and The Preprocessor
