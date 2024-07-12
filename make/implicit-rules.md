# Implicit Rules

make has implicit rules for compiling and linking C programs. Much of the information we entered in our dependency rules can in fact be inferred by make. Consider the following rule, for example:

```makefile
intmath.o: intmath.c intmath.h
    $(CC) $(CFLAGS) -c intmath.c
```

We could have actually written it as:

```
intmath.o: intmath.h
```

And from observing that the target is intmath.o, makes would infer that it depends on intmath.c and that the command to build it is $(CC) $(CFLAGS) -c intmath.c. Of course, make cannot infer header file dependencies, so we still need to intmath.h as a dependency.&#x20;

Similarly, consider the rule for the executable:

```
testintmath: testintmath.o intmath.o
    $(CC) testintmath.o intmath.o -o testintmath
```

We could have written it as:

```
testintmath: intmath.o
```

And from observing that the executable is testintmath, make would infer that it depends on testintmath.o and that the command to build it is  $(CC) testintmath.o intmath.o -o testintmath. Note, however, that this only works since \<fill in>. If, for example, we named the executable testintmath1, make would assume it depends on testintmath1.o, which is of course incorrect.&#x20;

Here's what our makefile looks like incorporating these shortcuts:

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

testintmath: intmath.o

testintmath.o: intmath.h

intmath.o: intmath.h
```
