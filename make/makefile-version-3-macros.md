# Macros

Make has a macro facility that performs textual substitution, similar to the macro facility of the C preprocessor. To define a macro, add the following line to your makefile:

```makefile
MACRO_NAME = value
```

where `MACRO_NAME` is the name of the macro you’re defining and `value` is the value you’re assigning to it. To use the macro in the Makefile, enclose its name in `$()` , like so:

```makefile
$(MACRO_NAME)
```

When `make` encounters `$(MACRO_NAME)`, it will replace it with `value`. Note that parenthesis are optional if the macro is a single character.

Makefile version 3, shown below, illustrates three commonly used macros: `CC`, which specifies the compiler, `CFLAGS`, which specifies compiler options, and `LDFLAGS`, which specifies linker options. Notice that several versions of each macro is defined, with all but the ones in use commented out.&#x20;

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
* `CC` is actually a predefined macro, meaning make sets it automatically. By default, `CC` is set to `cc`, which is not what we want; thus, we change it to gcc.
* If an undefined macro is used, it will be substituted with a blank space. Thus, lines 4 and 8 of our makefile (where we "defined" `CFLAGS` and `LDFLAGS`) are actually redundant. We could have put them in the rules without defining them as an empty string, since that's the default.&#x20;
{% endhint %}
