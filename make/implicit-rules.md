# Advanced Features

The current features we've covered capture the core of make. And are all you need to know about make. However, make has other features. Many of them are confusing and make makefiles much less readable, but they are often used in real-world makefiles, so it's useful to have a working familiarity with them.&#x20;

#### Automatic Macros&#x20;

make has macros that can be used in each rule. They're like regular predefined macros except that they're only defined when used in rules and their definition depends on the rule they're used in. Below is a few of the commonly used automatic macros. Note that since each of these macros is only a single character, they can be referenced by simply prefixing their name with a $.&#x20;

<table><thead><tr><th width="109">Macro</th><th width="239">Meaning</th><th>Example</th></tr></thead><tbody><tr><td><code>^</code></td><td>All the dependencies.</td><td><pre class="language-makefile"><code class="lang-makefile">testintmath: testintmath.o intmath.o
    $(CC) $(LDFLAGS) $^ -o testintmath
</code></pre></td></tr><tr><td><code>@</code></td><td>The target.</td><td><pre class="language-makefile"><code class="lang-makefile">testintmath: testintmath.o intmath.o
    $(CC) $(LDFLAGS) $^ -o $@
</code></pre></td></tr><tr><td><code>^</code></td><td>The first dependency.</td><td><pre class="language-makefile"><code class="lang-makefile">intmath.o: intmath.c intmath.h
    $(CC) $(CFLAGS) -c $^
</code></pre></td></tr><tr><td><code>?</code></td><td>Dependencies newer than the target.</td><td><pre class="language-makefile"><code class="lang-makefile">
</code></pre></td></tr></tbody></table>

#### Pattern Rules

#### Inference Rules

`make` has inference rules for compiling and linking C programs. Much of the information we entered in our makefile can in fact be inferred by `make`. Consider the following rule, for example:

```makefile
intmath.o: intmath.c intmath.h
    $(CC) $(CFLAGS) -c intmath.c
```

We could have actually written it as:

```
intmath.o: intmath.h
```

And from observing that the target is `intmath.o`, `make` would infer that it depends on `intmath.c` and that the command to build it is `$(CC) $(CFLAGS) -c intmath.c`. Of course, `make` cannot infer header file dependencies, so we still need to list `intmath.h` as a dependency.&#x20;

Similarly, consider the rule for the executable:

```
testintmath: testintmath.o intmath.o
    $(CC) $(LDFLAGS) testintmath.o intmath.o -o testintmath
```

We could have written it as:

```
testintmath: intmath.o
```

And from observing that the executable is `testintmath`, make would infer that it depends on `testintmath.o` and that the command to build it is `$(CC) $(LDFLAGS) testintmath.o intmath.o -o testintmath`.

Note, however, that this only works since the executable (`testintmath`)  has the same prefix of one of the object files (`testintmath.o`). If not, this wouldn't work. For example, if the executable were named `testintmath1`, `make` would incorrectly assume it depends on `testintmath1.o`.

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

intmath.o: intmath.h

testintmath.o: intmath.h 
```
{% endcode %}



#### Special Targets

Specicial targets are builtk in&#x20;
