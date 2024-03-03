# Makefile Version 1: Basic



<figure><img src="../../.gitbook/assets/Group 28 (1).png" alt="" width="563"><figcaption></figcaption></figure>



The transition from a dependency graph to a Makefile is intuitive and straightforward.

1. Create a rule for each object file and for the executable. In our dependency graph, they're circled in red.&#x20;
2. **Executable Rule**:
   * Target: `testintmath`
   * Dependencies: `testintmath.o` and `intmath.o`
   * Command: Link the object files to create the executable. Use `gcc testintmath.o intmath.o -o testintmath` to compile.
3. **Object File Rules**:
   * For `testintmath.o`:
     * Target: `testintmath.o`
     * Dependencies: `testintmath.c` and `intmath.h`
     * Command: Compile the source file into an object file with `gcc -c testintmath.c`.
   * For `intmath.o`:
     * Target: `intmath.o`
     * Dependencies: `intmath.c` and `intmath.h`
     * Command: Compile the source file into an object file with `gcc -c intmath.c`.

```makefile
testintmath: testintmath.o intmath.o
     gcc testintmath.o intmath.o -o 

testintmath.o: testintmath.c intmath.h
     gcc -c testintmath.c

intmath.o: intmath.c intmath.h
     gcc -c intmath.c
```

## Running a makefile

To run a makefile, we use the `make` command in the terminal, followed by the name of the target we want to build. To build `testintmath`, we invoke:

```
make testintmath
```

Alternatively, to build testintmath we can invoke `make` without specifying a target:

```
make
```

Since if no target is specified, make will default to the first target in the makefile, which in our case is testintmath.&#x20;

### Our makefile in Action

Let's now examine how make processes our makefile at various points of development. We'll consider three cases.

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



{% hint style="info" %}
#### Makefile version 0

First up is what we're calling Version 0. It's a bit unconventional – it does the job, but it's not the model of a well-crafted makefile. Think of it as our "what not to do" guide. By seeing the flaws and missteps in Version 0, you'll get a clearer picture of what makes a makefile effective and well-structured. Here's how it looks:

{% code title="Makefile version 0" %}
```
testintmath: testintmath.c intmath.c intmath.h
    gcc intmath.c testintmath.c -o testintmath
```
{% endcode %}

The first line declares a target `testintmath`, which depends on `testintmath.c`, `intmath.c`, and `intmath.h`. This means that if any of these files change, `make` will rebuild `testintmath`. The second line is the command that `make` will execute to build testintmath.&#x20;

Despite being functional, Version 0 is structurally flawed, since it re-compiles the entire program whenever a change is introduced to any one of the dependencies--intmath.c, testintmath.c, or intmath.h. However, as we know from...
{% endhint %}