# Advanced Features

The current features we've covered are all you need to know about make. However, make has other features. Many of them are confusing and make makefiles much less readable, but they are often used in real-world makefiles, so it's useful to have a working familiarity with them.&#x20;

#### Automatic Macros&#x20;

make has macros that can be used in each rule. They're like regular macros except they're defined my make and their definition depends on context.

* $@ - Evaluates to current target. Example:

```
testintmath: testintmath.o intmath.o
    $(CC) $(LDFLAGS) testintmath.o intmath.o -o $@
```

* $? - Evaluate to the list of prerequisites that are newer than the current target. Example:

```
testintmath.o: testintmath.c intmath.h
    $(CC) -c $(CFLAGS) $< -o testintmath.o
```

* In an inference rule, the $< macro shall evaluate to the filename whose existence allowed the inference rule to be chosen for the target. Example:

```
testintmath: testintmath.o intmath.o
    $(CC) $(LDFLAGS) $^ -o $@
```

* The $\* macro shall evaluate to the current target name with its suffix deleted. It shall be evaluated at least for inference rules. Example:

```
testintmath: testintmath.o intmath.o
    @echo "Rebuilding $@ because $? have changed"
    $(CC) $(LDFLAGS) $^ -o $@
```

#### Implicit Rules

`make` has implicit rules for compiling and linking C programs. Much of the information we entered in our makefile can in fact be inferred by `make`. Consider the following rule, for example:

```makefile
intmath.o: intmath.c intmath.h
    $(CC) $(CFLAGS) -c intmath.c
```

We could have actually written it as:

```
intmath.o: intmath.h
```

And from observing that the target is `intmath.o`, `make` would infer that it depends on `intmath.c` and that the command to build it is `$(CC) $(CFLAGS) -c intmath.c`. Of course, `make` cannot infer header file dependencies, so we still need to `intmath.h` as a dependency.&#x20;

Similarly, consider the rule for the executable:

```
testintmath: testintmath.o intmath.o
    $(CC) $(LDFLAGS) testintmath.o intmath.o -o testintmath
```

We could have written it as:

```
testintmath: intmath.o
```

And from observing that the executable is `testintmath`, make would infer that it depends on `testintmath.o` and that the command to build it is.



&#x20;`$(CC) testintmath.o intmath.o -o testintmath`. Note, however, that this only works since the executable (`testintmath`)  has the same prefix of one of the object files (`testintmath.o`). If not, this wouldn't work. For example, if the executable were named `testintmath1`, `make` would incorrectly assume it depends on `testintmath1.o`.

Here's what our makefile looks like after incorporating these shortcuts:

{% code title="makefile version 4" %}
```makefile
# Macros
CC = gcc
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

testintmath: intmath.o

testintmath.o: intmath.h

intmath.o: intmath.h
```
{% endcode %}

There is no reason to use implicit rules, since they tend to make Makefiles confusing and difficult to interpret. However, it's useful to be aware of them, since many Makefiles you'll encounter do make use of them.&#x20;
