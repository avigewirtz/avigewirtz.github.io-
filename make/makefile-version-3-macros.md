# Macros

Make has a macro facility that performs textual substitution, similar to the macro facility of the C preprocessor. To define a macro, add the following line to your makefile:

```makefile
MACRO_NAME = value
```

where `MACRO_NAME` is the name of the macro you’re defining and `value` is the value you’re assigning to it. To use the macro in the Makefile, enclose its name in `$()` , like so:

```makefile
$(MACRO_NAME)
```

When `make` encounters `$(MACRO_NAME)`, it will replace it with `value`.

Makefile version 3, shown below, illustrates three commonly used macros: `CC`, used to specify the compiler, `CFLAGS`, used to specify compiler options, and `LDFLAGS`, used to specify linker options. Notice that we define several values for each macro, with all but the ones we're currently using commented out.

{% code title="Makefile version 3" lineNumbers="true" %}
```makefile
# Macros
CC = gcc
# CC = clang
CFLAGS =
# CFLAGS = -g
# CFLAGS = -D NDEBUG
# CFLAGS = -D NDEBUG -O
LDFLAGS = 
# LDFLAGS = -g

# Dependency rules for non-file targets
all: testintmath
clobber: clean
    rm -f *~ \#*\#
clean:
    rm -f testintmath *.o
    
# Dependency rules for file targets
testintmath: testintmath.o intmath.o
    $(CC) $(LDFLAGS) testintmath.o intmath.o -o testintmath
testintmath.o: testintmath.c intmath.h
    $(CC) -c $(CFLAGS) testintmath.c
intmath.o: intmath.c intmath.h
    $(CC) -c $(CFLAGS) intmath.c
```
{% endcode %}

The benefit of using macros is that it allows for easy and consistent updates across the entire Makefile. For example, if we want to change the compiler to `clang`, all we need to do is change `CC` to `clang`, instead of manually changing every compilation command.

{% hint style="info" %}
`CC`, `CFLAGS` and `LDFLAGS` are actually predefined macros, meaning they are recognized by `make` even if we don't explicitly define them. By default, `CC` is set to `cc`, while `CFLAGS` and `LDFLAGS` are an empty string. Thus, lines 4 and 8 of our makefile (where we "defined" `CFLAGS` and `LDFLAGS`) are actually redundant. (As to why `make` predefines `CFLAGS` and `LDFLAGS` to empty strings, this is so it can use them in implicit rules without causing an error. This will make sense after reading [Implicit Rules](implicit-rules.md)).
{% endhint %}
