# Advanced Features

The features we've discussed so far cover the basics of `make` and are enough to use it effectively. However, make has other features, such as automatic macros and implicit rules, which are commonly used in real-world Makefiles.  Therefore, while many of these features can be confusing and make Makefiles less readable, they are useful to have a working familiarity with them.

#### Automatic Macros&#x20;

make has macros that can be used in each rule. They're like regular predefined macros except that they're only defined when used in rules and their definition depends on the rule they're used in. Below is a few of the commonly used automatic macros. Note that since each of these macros is only a single character, they can be referenced by simply prefixing their name with a $.&#x20;

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

Here is our makefile with explicit filenames replaced by the appropriate automatic variables:

{% code title="Makefile version 4" %}
```
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

`make` has built-in rules for compiling and linking C programs. Much of the information we entered in our makefile can in fact be inferred by `make`. Consider the following rule, for example:

```makefile
intmath.o: intmath.c intmath.h
    $(CC) $(CFLAGS) -c intmath.c
```

We could have actually written it as:

```
intmath.o: intmath.h
```

And from observing that the target is `intmath.o`, `make` would infer that it depends on `intmath.c` and that the command to build it is (roughly) `$(CC) $(CFLAGS) -c intmath.c`. Of course, `make` cannot infer header file dependencies, so we still need to list `intmath.h` as a dependency.&#x20;

Similarly, consider the rule for the executable:

```
testintmath: testintmath.o intmath.o
    $(CC) $(LDFLAGS) testintmath.o intmath.o -o testintmath
```

We could have written it as:

```
testintmath: intmath.o
```

And from observing that the executable is `testintmath`, make would infer that it depends on `testintmath.o` and that the command to build it is (roughly) `$(CC) $(LDFLAGS) testintmath.o intmath.o -o testintmath`.

{% hint style="info" %}
Note, however, that this only works since the executable (`testintmath`)  has the same prefix of one of the object files (`testintmath.o`). If not, this wouldn't work. For example, if the executable were named `testintmath1`, `make` would incorrectly assume it depends on `testintmath1.o`.
{% endhint %}

By using these built-in rules our Makefile can be reduced to:

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

Running this makefile:

```
$ touch intmath.h
$ make
gcc    -c -o testintmath.o testintmath.c
gcc    -c -o intmath.o intmath.c
gcc   testintmath.o intmath.o   -o testintmath
$
```

{% hint style="info" %}


The implicit rules we discussed are all instances of built-in pattern rules. Pattern rules use wildcards instead of explicit filenames. This allows make to apply the rule any time a target file matching the pattern needs to updated.

The percent character in a pattern rule is roughly equivalent to \* in a Unix shell. It represents any number of any characters. This makefile works because of two built-in pattern rules. The first specifies how to compile a .o file from a .c file:

```
     %.o: %.c
             $(COMPILE.c) $(OUTPUT_OPTION) $<
```

where:

```
COMPILE.c = $(CC) $(CFLAGS) $(CPPFLAGS) $(TARGET_ARCH) -c
OUTPUT_OPTION = -o $@
```

The second specifies how to generate a file with no suffix (always an executable) from a .o file:

```
     %: %.o
             $(LINK.o) $^ $(LOADLIBES) $(LDLIBS) -o $@
```

where:

```
LINK.o = $(CC) $(LDFLAGS) $(TARGET_ARCH)
```
{% endhint %}
