# Macros

Make has a macro facility that performs textual substitution, similar to the `#define` directive in C. This allows you to define a shorthand term for a longer sequence of characters and to use the shorthand in your program. To define a macro, you simply assign a value to a name. For example:

```makefile
CC = gcc217
```

Here, `CC` is the name of the macro, and `gcc217` is the value assigned to it. Once a macro is defined, you can use it anywhere in the Makefile by referencing its name prefixed with a dollar sign and enclosed in parentheses or curly braces. For instance:

```makefile
intmath.o: intmath.c intmath.h
    $(CC) -c intmath.c
```

When this rule is processed, `$(CC)` will be replaced with `gcc217`.

## Common macros

Common macros include CC, which we just covered, and CFLAGS, which is used to specify command line options to invoke the compiler with. The benefit of using these macros is we can change the compiler or compiler flags by modifying a single line in the Makefile, rather than having to modify each command individually. Let's enhance our makefile by adding these two macros:

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
