# Advanced Features

The features we've discussed so far cover the basics of `make` and give you enough information to use it effectively. However, make has other features, such as automatic macros and implicit rules, which are commonly used in real-world Makefiles. While many of these features can be confusing and make Makefiles less readable, it is useful to have a working familiarity with them.

#### Automatic Macros

`make` has _automatic_ macros (also called automatic variables) that can be used in a rule's command. Each of these macros expands to one or more filenames. They're useful as shortcuts but are primarily designed to enable pattern rules (discussed below). The following table lists a few of the commonly used automatic macros. Note that since automatic macros are all a single character, they can be referenced by simply prefixing their name with a `$`.

<table><thead><tr><th width="109">Macro</th><th width="239">Meaning</th><th>Example</th></tr></thead><tbody><tr><td><code>^</code></td><td>List of all dependencies.</td><td><pre class="language-makefile"><code class="lang-makefile">testintmath: testintmath.o intmath.o
    $(CC) $(LDFLAGS) $^ -o testintmath
</code></pre></td></tr><tr><td><code>@</code></td><td>The target.</td><td><pre class="language-makefile"><code class="lang-makefile">testintmath: testintmath.o intmath.o
    $(CC) $(LDFLAGS) $^ -o $@
</code></pre></td></tr><tr><td><code>&#x3C;</code></td><td>The first dependency.</td><td><pre class="language-makefile"><code class="lang-makefile">intmath.o: intmath.c intmath.h
    $(CC) $(CFLAGS) -c $&#x3C;
</code></pre></td></tr><tr><td><code>?</code></td><td>List of all dependencies newer than the target.</td><td><pre class="language-makefile"><code class="lang-makefile">intmath.o: intmath.c intmath.h
    $(CC) $(CFLAGS) -c $&#x3C;
    @echo "Modified dependency(ies): $?"
</code></pre></td></tr></tbody></table>

Here is our Makefile with explicit filenames in each rule replaced by the appropriate automatic variables:

{% code title="Makefile version 4" %}
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
    
testintmath: testintmath.o intmath.o
    $(CC) $(LDFLAGS) $^ -o @
    
testintmath.o: testintmath.c intmath.h
    $(CC) $(CFLAGS) -c $<
    
intmath.o: intmath.c intmath.h
    $(CC) $(CFLAGS) -c $<
```
{% endcode %}

#### Implicit Rules

`make` has built-in rules for compiling and linking C programs. Much of the information we entered in our makefile can in fact be inferred by `make`. Consider the rule for building `intmath.o`:

```makefile
intmath.o: intmath.c intmath.h
    $(CC) $(CFLAGS) -c intmath.c
```

We could have actually written it as:

```makefile
intmath.o: intmath.h
```

And from observing that the target is `intmath.o`, `make` would infer that it depends on `intmath.c` and that the command to build it is (roughly) `$(CC) $(CFLAGS) -c intmath.c`. Of course, `make` cannot infer header file dependencies, so we still need to list `intmath.h` as a dependency.

Similarly, consider the rule for building `testintmath`:

```makefile
testintmath: testintmath.o intmath.o
    $(CC) $(LDFLAGS) testintmath.o intmath.o -o testintmath
```

We could have written it as:

```makefile
testintmath: intmath.o
```

And from observing that the executable is `testintmath`, `make` would infer that it depends on `testintmath.o` and that the command to build it is (roughly) `$(CC) $(LDFLAGS) testintmath.o intmath.o -o testintmath`.

{% hint style="warning" %}
Note that an implicit rule may only be used for an executable if the executable has the same name as one of the object files.
{% endhint %}

By using these implicit rules our Makefile can be reduced to:

{% code title="makefile version 5" %}
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

intmath.o: intmath.h

testintmath.o: intmath.h 
```
{% endcode %}

In fact, we can reduce this Makefile further by combining the two object files rules into a single rule:&#x20;

```makefile
testintmath.o intmath.o: intmath.h 
```

Running this Makefile, we can see the commands that are executed by `make`:

```bash
$ touch intmath.h
$ make
gcc    -c -o testintmath.o testintmath.c
gcc    -c -o intmath.o intmath.c
gcc   testintmath.o intmath.o   -o testintmath
$
```

{% hint style="info" %}
**Pattern Rules**

The implicit rules we discussed are all instances of built-in pattern rules. Pattern rules use wildcards instead of explicit filenames. This allows make to apply the rule any time a target file matching the pattern needs to updated.

The percent character in a pattern rule is roughly equivalent to \* in a Unix shell. It represents any number of any characters. This makefile works because of two built-in pattern rules. The first specifies how to compile a .o file from a .c file:

```makefile
     %.o: %.c
             $(COMPILE.c) $(OUTPUT_OPTION) $<
```

where:

```makefile
COMPILE.c = $(CC) $(CFLAGS) $(CPPFLAGS) $(TARGET_ARCH) -c
OUTPUT_OPTION = -o $@
```

The second specifies how to generate a file with no suffix (always an executable) from a .o file:

```makefile
     %: %.o
             $(LINK.o) $^ $(LOADLIBES) $(LDLIBS) -o $@
```

where:

```makefile
LINK.o = $(CC) $(LDFLAGS) $(TARGET_ARCH)
```
{% endhint %}
