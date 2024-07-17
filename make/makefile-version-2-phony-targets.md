# Phony targets

In our current makefile, each rule's target is the name of a file that is built when the rule's command is executed.&#x20;











For example, in the following rule:

```makefile
intmath.o: intmath.c intmath.h
    gcc -c intmath.c
```

The target is `intmath.o`, which is built when the command `gcc -c intmath.c` is executed. Recall that this command will be executed if either `intmath.o` does not exist or if one of its dependencies have a more recent modification timestamp.

A flexible feature of `make` is that it does not require that the target actually represent a file. Instead, it can represent a label for an arbitrary command or action you want `make` to execute. Such a target is called a _phony target_. Phony targets are easiest to illustrate by example, so let's jump right into makefile version 2, which contains three phony targets: all, clean, and clobber. Don't worry about what they mean or how they work for now. We'll go over them one-by-one.&#x20;

{% code title="makefile version 2" lineNumbers="true" %}
```makefile
# Dependency rules for non-file targets

# Default target (i.e., target to use when make is invoked without specifying a target)
all: testintmath
  
# Deletes all object files (.o) and the executable 
clean:
    rm -f testintmath *.o
  
# Extends clean by also deleting Emacs backup and autosave files ('*~' specifies 
# all files that end with a '~', and '\#*\#' specifies all files that start and end with a '#')
clobber: clean
    rm -f *~ \#*\# 
  
# Dependency rules for file targets
testintmath: testintmath.o intmath.o
    gcc testintmath.o intmath.o –o testintmath
  
testintmath.o: testintmath.c intmath.h
    gcc -c testintmath.c
  
intmath.o: intmath.c intmath.h
    gcc -c intmath.c
```
{% endcode %}

Let's start with the rule for `clean`:

```
clean:
    rm -f testintmath *.o
```

Notice a couple of things about this rule. First, `clean`, does not represent a file—that is, there is no file in our directory named `clean`, and the command `rm -f testintmath *.o` does not create such a file. Second, it contains no dependencies.&#x20;

Thus, the semantic are as follows: if clean does not exist, run the command rm -f testintmath \*.o. We would think this might cause an error since clean isn't created, but make does not. Make does not actauilly verify the cxlean is created.&#x20;





&#x20;In fact, it serves quite an opposite purpose--to delete the object files and the executable. (Also notice that the target does not have any dependencies. That's perfectly valid, as dependencies are optional. Make will simply skip the dependency checking step and determine whether to run the command based solely on the existence of clean.)



Here's how it works. When `make` processes this rule, it assumes that `clean` represents a file. It thus looks for a file named `hello` in the working directory. Because it does not find one, it determines that `hello` needs to be built, and it thus executes the command `echo "Hello, world!"`. At this point, `make` considers its job complete. It does not care whether a file named `hello` is in fact created.

Here's how it works. Make assumes that all targets and prerequisites represent files.&#x20;



In our current makefile, each rule's target is the name of a file that is built when the rule's command is executed. For example, in the following rule:

```makefile
intmath.o: intmath.c intmath.h
    gcc -c intmath.c
```

The target is `intmath.o`, which is built when the command `gcc -c intmath.c` is executed. Recall that this command will be executed if either `intmath.o` does not exist or if one of its dependencies have a more recent modification timestamp.

A flexible feature of `make` is that it does not require that the target actually represent a file. Instead, it can represent a label for an arbitrary command or action you want `make` to execute. Such a target is called a _phony target_. Consider the following rule:

```makefile
hello: 
    echo "Hello, world!" 
```

The target, `hello`, does not represent a file—that is, there is no file in our directory named `hello`, and the command `echo "hello, world"` does not create such a file. (Also notice that the target does not have any dependencies. That's perfectly valid, as dependencies are optional.) What would happen if we were to add this rule to our Makefile and invoke it? Let's give it a shot:

```bash
$ make hello
echo "Hello, world!"
Hello, world!
$
```

We see that `make` executes the command `echo "Hello, world!"`, printing `Hello, world!` on stdout. The fact that this command does not create a file named `hello` does not cause an error.

Here's how it works. When `make` processes this rule, it assumes that `hello` represents a file. It thus looks for a file named `hello` in the working directory. Because it does not find one, it determines that `hello` needs to be built, and it thus executes the command `echo "Hello, world!"`. At this point, `make` considers its job complete. It does not care whether a file named `hello` is in fact created.

A few things are important things are importance to recognize:

1. Because this rule will never create a file named `hello`, it will always be considered out-of-date. Thus, we can run `make hello` as many times as we'd like, and, each time, `make` will execute the command `echo "Hello, world!"`. For example, if we run `make hello` three times in a row:

```bash
$ make hello
echo "Hello, world!"
Hello, world!
$ make hello
echo "Hello, world!"
Hello, world!
$ make hello
echo "Hello, world!"
Hello, world!
$
```

2. This rule will never be invoked unless we explicitly specify it in the command line.
3. This scheme only works if there is in fact never a file named `hello` in the working directory. If there is such a file, it will always be considered up to date, and running `make hello` will always yield:

```makefile
$ make hello
make: `hello' is up to date.
$
```

GNU Make offers a simple solution to guard against this potential issue. Just declare `hello` to be phony, like so:

```makefile
.PHONY: hello
```

With this declaration, `make hello` will always run the specified command, even if there is a file named `hello`.

#### Commonly Used Phony Targets

Of course, the `hello` phony target is not particularly useful. In real-world makefiles, the following three phony targets are commonly used: `all`, `clean`, and `clobber`.

* `all`: This should be the default target..To create the final executable binary file(s), typically the default target in the makefile.
* `clean`: To delete all `.o` files and executable binary file(s).
* `clobber`: To extend clean by also deleting also build related files, such as Emacs backup files.

Here is Makefile version 2, which incorporates these 3 phony targets. Note that the order of the rules does not matter, except for the first tule, which serves as the default rule. Here, the first rule is `all`.

{% code title="makefile version 2" %}
```makefile
# Dependency rules for non-file targets

.PHONY: all clean clobber
# Default target (i.e., target to use when make is invoked without specifying a target)
all: testintmath
  
# Deletes all object files (.o) and the executable 
clean:
  rm -f testintmath *.o
  
# Extends clean by also deleting Emacs backup and autosave files ('*~' specifies 
# all files that end with a '~', and '\#*\#' specifies all files that start and end with a '#')
clobber: clean
  rm -f *~ \#*\# 
  
# Dependency rules for file targets
testintmath: testintmath.o intmath.o
  gcc testintmath.o intmath.o –o testintmath
  
testintmath.o: testintmath.c intmath.h
  gcc -c testintmath.c
  
intmath.o: intmath.c intmath.h
  gcc -c intmath.c
```
{% endcode %}

with these updates, running our makefile is the same as before. To build the entire program, we run make.

To delete...

{% hint style="info" %}
**Purpose of the 'all' target**

You might be wondering what purpose the `all` target serves in our program compared to simply using `testintmath` as the default target. Truthfully, it doesn't serve any real purpose, except perhaps for accommodating users who might invoke `make all` out of habit.

The real purpose of `all` is to group multiple independent targets and effectively make them all default targets. For example, suppose we have a project with two executables:`hello1` and `hello2`. Making `hello1` and `hello2` dependencies of `all` effectively makes them both default targets (which will be triggered when we run `make`).

```makefile
all: hello1 hello2

hello1: hello1.o
	gcc hello1.o -o hello1
	
hello2: hello2.o
	gcc hello2.o -o hello2

hello1.o: hello1.c
	gcc -c hello1.c

hello2.o: hello2.c
	gcc -c hello2.c
```
{% endhint %}
