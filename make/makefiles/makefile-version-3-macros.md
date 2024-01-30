# Macros

Make has a macro facility that performs textual substitution, which is similar to the `#define` directive in C.

**Defining a Macro**

To define a macro, you simply assign a value to a name. For example:

```makefile
CC = gcc217
```

Here, `CC` is the name of the macro, and `gcc217` is the value assigned to it.&#x20;

**Using a Macro**

Once a macro is defined, you can use it anywhere in the Makefile by referencing its name prefixed with a dollar sign and enclosed in parentheses or curly braces. For instance:

```makefile
intmath.o: intmath.c intmath.h
    $(CC) -c intmath.c
```

In this rule, `$(CC)` will be replaced by `gcc217` when the Makefile is processed. This means the command executed will be `gcc217 -c intmath.c`.

#### Common Use Cases

Macros in Makefiles are commonly used to specify key components of build commands, such as the compiler and compiler flags. This approach allows for centralized management of these settings. By modifying the macro definition, you can alter the build commands consistently throughout the entire Makefile. Here is an updated version of our Makefile that incorporates this concept:

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

This updated Makefile uses two macros for build commands: `CC` and `CFLAGS`. `CC` is defined as `gcc217`, and `CFLAGS` is initially left blank, with various commented-out options provided. These commented versions allow for easy swapping. For example, if we want `CFLAGS` to include the `-D NDEBUG` flag, we simply comment out the current `CFLAGS` line (line 4) and uncomment line 7. By doing this, the change in compiler flags is applied throughout the Makefile wherever `$(CFLAGS)` is used,
