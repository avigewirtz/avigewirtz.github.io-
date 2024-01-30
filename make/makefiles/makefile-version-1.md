# Makefile version 1

#### Makefile version 1

In this section, we will construct a well-organized makefile that leverages the benefits of partial builds. To effectively draft this makefile, it's beneficial to visualize the dependency graph. As a point of reference, the dependency graph for "testintmath" is illustrated in Figure 1.

<figure><img src="../../.gitbook/assets/dependency_graph (1).png" alt=""><figcaption></figcaption></figure>

When crafting a proper makefile, we adhere to certain key principles:

1. We establish a rule for each object file and the executable.
2. Each object file is dependent on its corresponding .c file and any .h files that are included, whether directly or indirectly, in the .c file.
3. Object files are independent of:
   * Any other .c files.
   * Any other .o files.
4. Each executable:
   * Relies on the .o files that form it.
   * Is not dependent on any .c or .h files.

In practical terms, our makefile will include three rules: one for the "testintmath" executable, one for the "testintmath.o" object file, and another for the "intmath.o" object file. For the "testintmath" executable's dependencies, we only list the object files "testintmath.o" and "intmath.o", excluding any .c or .h files. Regarding the "testintmath.o" dependencies, we include its .c file, "testintmath.c", and any header files it incorporates, which in this case is "intmath.h". Likewise, the dependencies for "intmath.o" are "intmath.c" and "intmath.h".

Following these guidelines, we arrive at a straightforward yet well-structured makefile:

```makefile
makefileCopy codetestintmath: testintmath.o intmath.o
    gcc testintmath.o intmath.o -o testintmath

testintmath.o: testintmath.c intmath.h
    gcc -c testintmath.c

intmath.o: intmath.c intmath.h
    gcc -c intmath.c
```

This structure ensures efficient and accurate builds by clearly defining dependencies and separating the compilation of individual components.

### Our makefile in Action

Let's now examine how make processes our makefile. We'll consider three cases.

<figure><img src="../../.gitbook/assets/Group 19 (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/Group 20.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/Group 22.png" alt=""><figcaption></figcaption></figure>

## other points i want to make:

* You can add comments in a makefile by beginning the line with a # symbol. For example:

```
# this is a comment
```

* A rule can have multiple commands and targets. We won't cover such rules here.&#x20;
* The order in which rules appear in the makefile isn't signifigant, except for the first rule, which&#x20;
* doesn't process all rules. only ones&#x20;
