# Macros

Make has a macro facility that performs textual substitution, similar to the macro facility of the C preprocessor. To define a macro, add the following line to the top of your makefile:

```makefile
MACRO_NAME = value
```

Where `MACRO_NAME` is the name of the macro you’re defining and `value` is the value you’re assigning to it. To subsequently use the macro in the Makefile, enclose its name in `$()` , like so:

```makefile
$(MACRO_NAME)
```

When `make` encounters `$(MACRO_NAME)`, it will replace it with `value`.

Makefile version 3, shown below, illustrates two commonly used macros: `CC`, used to specify the compiler, and `CFLAGS`, used to specify compiler options. Notice that we define several values for each macro, with all but the ones we're currently using commented out.

{% code title="Makefile version 3" lineNumbers="true" %}
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
    $(CC) testintmath.o intmath.o -o testintmath
testintmath.o: testintmath.c intmath.h
    $(CC) $(CFLAGS) -c testintmath.c
intmath.o: intmath.c intmath.h
    $(CC) $(CFLAGS) -c intmath.c
```
{% endcode %}

The benefit of using macros is that it allows for easy and consistent updates across the entire Makefile. For example, if we want to change the compiler to `clang`, all we need to do is change `CC` to `clang`, instead of manually changing every compilation command.

{% hint style="info" %}
`CC` and `CFLAGS` are actually predefined macros, meaning they are recognized by Make even if we don't explicitly define them. By default, `CC` is set to `cc`, and `CFLAGS` is an empty string. Thus, the `CFLAGS =` definition on line 4 is actually redundant. (As to why Make predefines `CFLAGS` to an empty string, this is so it can use it in implicit rules without causing an error. This will make sense after reading [Implicit Rules](implicit-rules.md)).
{% endhint %}
