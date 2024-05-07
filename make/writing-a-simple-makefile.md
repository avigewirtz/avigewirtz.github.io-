# Writing a Simple Makefile

The transition from a dependency graph to makefile is quite straightforward. We'll describe how it's done for the `testintmath` program, whose dependency graph is shown in Figure 12.&#x20;

<figure><img src="../.gitbook/assets/Group 125 (1).png" alt="" width="563"><figcaption><p>Figure 12.3: testintmath's dependency graph</p></figcaption></figure>

### Dependency Rules

We create a what is known as a dependency rule for each file that is created via a build. In make terminology, such files are know as targets. Targets are easy to identify, since they correspond to nodes that have children. In our case, we have three targets: intmath.o, testintmath.o, and testintmath. Dependency rules have the following syntax:

```
target: dependencies
<tab> command
```

* **Dependencies** . These are the files that the target _directly_ depends on (e.g., `testintmath` directly depends on `testintmath.o` and `intmath.o`).  We do not include indirect dependencies.&#x20;
* **Command**. This is the command make invokes to build the target. Note that it must be preceded by a Tab character.&#x20;

This results in the following Makefile:&#x20;

```makefile
testintmath: testintmath.o intmath.o
    gcc217 testintmath.o intmath.o -o testintmath

testintmath.o: testintmath.c intmath.h
    gcc217 -c testintmath.c

intmath.o: intmath.c intmath.h
    gcc217 -c intmath.c
```

### Running our makefile

The general syntax to run a Makefile is:

```bash
make target
```

If you omit a target, `make` defaults to the first target in the makefile.&#x20;

To build `testintmath`, we can invoke `make` without specifying a target and 'make' will default to `testintmath`, since it's the first target in our Makefile:

```bash
make
```

If we wanted to build `intmath.o` alone, we'd invoke:

```bash
make intmath.o
```

{% hint style="info" %}
`make` does not read a makefile from top to bottom, processing all rules within it. It starts with the default rule or the rule specified on the command line, and then processes only the rules that are reachable from it.&#x20;
{% endhint %}
