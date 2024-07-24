# Macros

Make has a macro facility that performs textual substitution, similar to the macro facility of the C preprocessor. To define a macro, add the following line to your Makefile:

```makefile
MACRO_NAME = value
```

where `MACRO_NAME` is the name of the macro you’re defining and `value` is the value you’re assigning to it. To use the macro in the Makefile, enclose its name in `$()` , like so:

```makefile
$(MACRO_NAME)
```

When `make` encounters `$(MACRO_NAME)`, it will replace it with `value`.&#x20;

Makefile version 3, shown below, illustrates three commonly used macros: `CC`, `CFLAGS`, and `LDFLAGS`. These macros specify the compiler, compiler options, and linker options, respectively. The benefit of using macros is that it allows for easy and consistent updates across the entire Makefile. For example, if we want to change the compiler to `clang`, all we need to do is change `CC` to `clang`, instead of manually changing every compilation command.&#x20;

{% code title="Makefile version 3" lineNumbers="true" %}
```makefile
# Macros
CC = gcc
# CC = clang

# CFLAGS = -g
# CFLAGS = -D NDEBUG
# CFLAGS = -D NDEBUG -O

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

{% hint style="info" %}
**Properties of Macros**

* Some macros are predefined by make. In fact, CC is predefined to cc.&#x20;
* It is not an error to use an undefined macro; it simply expands to an empty string. This is why we use CLFAGS and LDFLAGS without defining them.&#x20;
* If the macro is a single character, you may call it without enclosing its name in parenthesis (e.g., `$X`). Thus, you could reference the variable `x` with ‘$x’
* Macros are expanded recursively. The effect is that...
{% endhint %}
