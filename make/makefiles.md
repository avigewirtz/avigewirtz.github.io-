# Makefiles

makefile is essentially a textual representation of a dependency graph. &#x20;

Here’s a simple makefile for our testintmath program:

{% code title="makefile" lineNumbers="true" %}
```makefile
testintmath: testintmath.o intmath.o
  gcc217 testintmath.o intmath.o –o testintmath
  
testintmath.o: testintmath.c intmath.h
  gcc217 -c testintmath.c
  
intmath.o: intmath.c intmath.h
  gcc217 -c intmath.c
```
{% endcode %}

* contains 3 groups of lines
*   each group is known as a rule. Each rule consists of a target, its dependencies, and a command to create the target from those dependencies. The format is as follows:

    ```
    target: dependencies
    <tab> command
    ```

    * **Target**: The file that the rule produces.
    * **Dependencies**: The files needed to build the target.
    * **Command**: The command that `make` will execute to generate the target.\


{% hint style="danger" %}
The first character of the line with the command must be an actual tab character (ASCII character 9). Cryptic error for failing to do so:

```
   *** missing separator.  Stop.
```
{% endhint %}



Let's go over the first rule in detail. &#x20;

{% code title="Rule 1" %}
```make
testintmath: testintmath.o intmath.o
    gcc217 testintmath.o intmath.o -o testintmath
```
{% endcode %}

* **Target**: `testintmath`
* **Dependencies**: `testintmath.o`, `intmath.o`
* **Command**: `gcc217 testintmath.o intmath.o -o testintmath`
* **Explanation**: This rule states that the executable `testintmath` depends on two object files: `testintmath.o` and `intmath.o`. The command to create `testintmath` is a call to the compiler `gcc217` to link these two object files. The `-o testintmath` part of the command specifies the output file name for the linked executable. This rule is triggered when either `testintmath.o` or `intmath.o` is newer than the `testintmath` executable, or when the executable does not exist.

\
