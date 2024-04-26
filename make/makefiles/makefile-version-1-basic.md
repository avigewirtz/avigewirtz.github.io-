# Writing a Makefile

The transition from a dependency graph to a Makefile is quite straightforward. Let's demonstrate how to write a makefile for testintmath, whose dependency graph is shown below.

<figure><img src="../../.gitbook/assets/Group 125 (1).png" alt=""><figcaption><p>Figure 12.3: testintmath's dependency graph</p></figcaption></figure>

The first step is to create a makefile in our program's directory. We can name it `Makefile`, `makefile`, or even `GNUmakefile` (assuming we're using GNU Make). GNU recommends `Makefile`.

Next, we populate the makefile with a textual representation of `testintmath`'s dependency graph. This consists of a _dependency rule_ for the executable (`testintmath`) and for each object file (`intmath.o`, `testintmath.o`). A dependency rule has the following syntax:

```
target: dependencies
<tab> command
```

* **Target**: The file you want to build (e.g., `testintmath`).
* **Dependencies**: The files that the target directly depends on (e.g., `intmath.o`, `testintmath.o`).
* **Command**: The command to build the target (e.g., `gcc217 intmath.o testintmath.o -o testintmath`). **Note:** The command must be preceded by a tab.

This results in the following makefile:

```makefile
testintmath: testintmath.o intmath.o
    gcc217 testintmath.o intmath.o -o testintmath

testintmath.o: testintmath.c intmath.h
    gcc217 -c testintmath.c

intmath.o: intmath.c intmath.h
    gcc217 -c intmath.c
```

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
**Note**: `make` does not read a makefile from top to bottom, processing all rules within it. It starts with the default rule or the rule specified on the command line, and then processes only the rules that are reachable from it.&#x20;
{% endhint %}
