# Makefile Version 3: Macros

Make has a macro facility that performs textual substitution, which is similar to the `#define` directive in C. To define a macro, you simply assign a value to a name. For example:

```makefile
CC = gcc217
```

Here, `CC` is the name of the macro, and `gcc217` is the value assigned to it. Once a macro is defined, you can use it anywhere in the Makefile by referencing its name prefixed with a dollar sign and enclosed in parentheses or curly braces. For instance:

```makefile
intmath.o: intmath.c intmath.h
    $(CC) -c intmath.c
```

In this rule, `$(CC)` will be replaced by `gcc217` when the Makefile is processed. This means the command executed will be `gcc217 -c intmath.c`.

Let's now update our makefile by taking advantage of macros:&#x20;

{% code title="makefile version 3" lineNumbers="true" %}
```makefile
# Macros
CC = gcc217
# CC = gcc217m
CFLAGS =
# CFLAGS = -g
# CFLAGS = -D NDEBUG
# CFLAGS = -D NDEBUG -O

# Dependency rules for non-file targets
all: testintmath
clobber: clean
    rm -f *~ \#*\#
clean:
    rm -f testintmath *.o
    
# Dependency rules for file targets
testintmath: testintmath.o intmath.o
    $(CC) $(CFLAGS) testintmath.o intmath.o -o testintmath
testintmath.o: testintmath.c intmath.h
    $(CC) $(CFLAGS) -c testintmath.c
intmath.o: intmath.c intmath.h
    $(CC) $(CFLAGS) -c intmath.c
```
{% endcode %}

This updated Makefile uses two macros for build commands: `CC` and `CFLAGS`, which specify the compiler and compiler flags respectively. `CC` is defined as `gcc217`, and `CFLAGS` is initially left blank, with various commented-out options provided, allowing for easy swapping. The benefit of these flags is we can change the compiler or compiler flags by modifying a single line in the Makefile, rather than having to edit each compilation command individually.
