# Linker

## The linker

Suppose we have a C program spread across 100 source files. This might seem like a lot, but many real-world applications have far more. One of these files contains the `main` function, the entry point of the program. This file calls functions defined in other files, which in turn use functions defined in additional files. Our program also uses functions in the C standard library. Our goal is to transform this collection of source files into a single executable file that can be loaded into memory and run.

Consider different approaches C compiler designers might use to build this program. One approach would be for the compiler to first combine all source files and the relevant C standard library code into a single, monolithic unit, and then translate that unit into machine code. The resulting file would be a single, cohesive unit, that can be loaded into memory as is and executed. Tis method would admittedyl present some challenges relating to implementing scoping and the like, but we can devise clever slutions for these.

The main problem with this approach is that the _entire_ program must be recompiled whenever _any_ change is made, no matter how small. This would be incredibly time-consuming and inefficient, especially for large projects.

The approach C compilers use is to first compile each source file separately into its own machine code file, known as a **relocatable object file**. A separate program called the **linker** then combines all the relocatable object files, including those from the C standard library, to generate a final, **executable object file**.&#x20;

#### Challenges of separate compilation

* addresses. solution is assembler leaves them blank for the linker to fill in.&#x20;
* type checking.  In separate compilation scheme, compiler only processes one file at a time. The problem, however, is that when a file calls a function defined in another file or uses a global variable from another file, the compiler has no way to see the definition beforehand. For example, For example, consider the following scenario:

{% code title="foo.c" %}
```c
int main() {
    bar(int 1, double 2);
    return 0;
}
```
{% endcode %}

Here, `foo.c` calls the `bar` function, defined elsewhere, but compiler has no way of knowing \<fill in>

The solution is that we insert prototype of all functions called at the top of the file.   \<now show updated example>. This way, compiler can type check. (For now, we'll assume you manually enter each prototype at top of file, as we'll see soon, however, preprocessor offers a more eficient method.)

