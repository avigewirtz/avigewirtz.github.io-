# Macros

Make has a macro facility that performs textual substitution, similar to the `#define` directive in C. The syntax to define a macro is as follows:

```makefile
MACRO_NAME = value
```

For example, to define the macro `CC` and assign it the value `gcc217`, you'd enter:&#x20;

```makefile
CC = gcc217
```

Once a macro is defined, you can use it anywhere in the Makefile by referencing its name prefixed with a dollar sign and enclosed in parentheses or curly braces. For example:

```makefile
intmath.o: intmath.c intmath.h
    $(CC) -c intmath.c
```

When this command is executed, make will replace `$(CC)` with `gcc217`.&#x20;



The benefit of this macro that we can easily substitute the compiler for many commands by changing a single value. For example, if we want to change the compiler to clang, you'd change CC = gcc217 to CC = clang, and then all commands with this macro will use clang. Typically, you create several versions of a macro, and then comment out all but the one you're currently using.&#x20;

Another commonly used macro is CFLAGS,  used to control the options the compiler is invoked with. Let's enhance our makefile by adding these the CC and CFLAGS macros:

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
