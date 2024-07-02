# Macros

Make has a macro facility that performs textual substitution, similar to the macro facility of the C preprocessor. To define a macro, add the following line to the top of your makefile:

```makefile
MACRO_NAME = value
```

Where `MACRO_NAME` is the name of the macro you’re defining and `value` is the value you’re assigning to it. To subsequently use the macro in the Makefile, enclose its name in `$()` (or `${}`), like so:

```makefile
$(MACRO_NAME)
```

When `make` encounters `$(MACRO_NAME)`, it will replace it with `value`.


Makefile version 3, shown below, integrates two commonly used macros: CC, which is used to specify the compiler, and CFLAGS, which is used to specify compiler options. 

{% code title="makefile version 3" lineNumbers="true" %}
```makefile
# Macros
CC = gcc217
# CC = clang
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

The benefit of using macros is it makes it extremely easy to change values. For example, if we want to change the compiler to `clang`, we'd change `CC = gcc217` to `CC = clang`, all we need to do is change CC to change, instead of changing every compilation command. 

Notice how we have several versions of each macro, with all but the one we're currently using commented out.&#x20;
