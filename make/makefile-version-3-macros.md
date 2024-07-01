# Macros

Make has a macro facility that performs textual substitution, similar to the macro facility in C. To define a macro, you add the following line to the top of your makefile:

```makefile
MACRO_NAME = value
```

Where MACRO_NAME is the name of the macro you’re defining and value is the value you’re assigning to it. For example, to define the macro `CC` and assign it the value `gcc217`, you'd add the following line to the top of your makefile: :&#x20;

```makefile
CC = gcc217
```

Once a macro is defined, you can use it anywhere in the Makefile by enclosing its name in $() or ${}:

```makefile
intmath.o: intmath.c intmath.h
    $(CC) -c intmath.c
```

When this command is executed, `make` will replace `$(CC)` with `gcc217`.&#x20;

Makefile version 3 illustrates macros. It contains the CC macro, which is used to control the compiler, and CFLAGS, which is used to control compiler options. 

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

The benefit of using macros is it makes it much more convenient to change values. For example, if we want to change the compiler to `clang`, we'd change `CC = gcc217` to `CC = clang`, all we need to do is change CC to change, instead of changing every compilation command. 

Notice how we have several versions of each macro, with all but the one we're currently using commented out.&#x20;
