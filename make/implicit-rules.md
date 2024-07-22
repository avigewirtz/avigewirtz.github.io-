# Advanced Features

The current features we've covered capture the core of make. And are all you need to know about make. However, make has other features. Many of them are confusing and make makefiles much less readable, but they are often used in real-world makefiles, so it's useful to have a working familiarity with them.&#x20;

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

Here is our makefile with explicit filenames replaced by the appropriate automatic variable:

```
testintmath: testintmath.o intmath.o
    $(CC) $(LDFLAGS) $^ -o @
    
testintmath.o: testintmath.c intmath.h
    $(CC) $(CFLAGS) -c $<
    
intmath.o: intmath.c intmath.h
    $(CC) $(CFLAGS) -c $<
```

#### Implicit Rules

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

By using these built-in rules our 17-line makefile can be reduced to:

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



{% hint style="info" %}
The built-in rules are all instances of pattern rules. A pattern rule looks like the nor- mal rules you have already seen except the stem of the file (the portion before the suf- fix) is represented by a % character. This makefile works because of three built-in rules. The first specifies how to compile a .o file from a .c file:

Pattern rules use wildcards instead of explicit filenames. This allows make to apply the rule any time a target file matching the pattern needs to updated.

The makefile examples we’ve been looking at are a bit verbose. For a small program of a dozen files or less we may not care, but for programs with hundreds or thou- sands of files, specifying each target, prerequisite, and command script becomes unworkable. Furthermore, the commands themselves represent duplicate code in our makefile. If the commands contain a bug or ever change, we would have to update all these rules. This can be a major maintenance problem and source of bugs.

Many programs that read one file type and output another conform to standard con- ventions. For instance, all C compilers assume that files that have a .c suffix contain C source code and that the object filename can be derived by replacing the .c suffix with .o (or .obj for some Windows compilers). In the previous chapter, we noticed that flex input files use the .l suffix and that flex generates .c files.

The percent character in a pattern rule is roughly equivalent to \* in a Unix shell. It represents any number of any characters.&#x20;

The percent character can be placed

GNU make 3.80 has about 90 built-in implicit rules. The built-in implicit rules are applied whenever a target is being considered and there is no explicit rule to update it. So using an implicit rule is easy: simply do not specify a command script when adding your target to the makefile. This causes make to search its built-in database to satisfy the target.

anywhere within the pattern but can occur only once. Here are some valid uses of percent:

```
     %,v
     s%.o
     wrapper_%
```
{% endhint %}















#### Special Targets

Specicial targets are builtk in&#x20;
