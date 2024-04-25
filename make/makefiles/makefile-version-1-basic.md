# Writing a Makefile

The transition from a dependency graph to a Makefile is quite straightforward. Let's demonstrate how to write a makefile for testintmath, whose dependency graph is shown below.

<figure><img src="../../.gitbook/assets/Group 28 (1).png" alt="" width="563"><figcaption><p>Figure 6: testintmath dependency graph</p></figcaption></figure>

The first step is to create a makefile in our program's directory. We can name it `Makefile`, `makefile`, or even `GNUmakefile` (assuming we're using GNU Make). GNU recommends `Makefile`.

Next, we populate the makefile with a textual representation of our program's dependency graph. This consists of a _dependency rule_ for each object file and for the executable. A dependency rule has the following syntax:

```
target: dependencies
<tab> command
```

* **Target**: The name of the file you want to build.
* **Dependencies**: The files that the target directly depends on.
* **Command**: The command to build the target. **Note:** The command must be preceded by a tab.

For our program, we have three targets: `testintmath`, `testintmath.o`, and `intmath.o`, resulting in three dependency rules. Our dependency graph makes it abundantly obvious which files each of these targets directly depend on: If file A points to file B, then A directly depends on B. In our case:

* `testintmath` directly depends on `intmath.o` and `testintmath.o`
* `intmath.o` directly depends on `intmath.c` and `intmath.h`
* `testintmath.o` directly depends on `testintmath.c` and `intmath.h`

This results in the following makefile:

```makefile
testintmath: testintmath.o intmath.o
    gcc217 testintmath.o intmath.o -o testintmath

testintmath.o: testintmath.c intmath.h
    gcc217 -c testintmath.c

intmath.o: intmath.c intmath.h
    gcc217 -c intmath.c
```

An important thing to notice is that a dependency can have its own rule. In other words, a file can be both a dependency and a target. This is the case for `testintmath.o` and `intmath.o`. As we'll soon see, make processes rules recursively.&#x20;

## Running our makefile

The general syntax of the `make` command is:

```bash
make target
```

where `target` is the name of the file you want `make` to build. If you omit a target, `make` defaults to the first target listed in the makefile.&#x20;

To build `testintmath`, we can invoke `make` without arguments and it'll default to `testintmath`:

```bash
make
```

To build `intmath.o` alone, we'd invoke:

```bash
make intmath.o
```

{% hint style="info" %}
**Note**: `make` does not read a makefile from top to bottom, processing all rules in it. It starts by processing the default rule or the rule specified on the command line, and then processes only the rules that are reachable from it.&#x20;
{% endhint %}
