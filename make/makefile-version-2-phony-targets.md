# Phony targets

In our makefile, each rule's target is the name of a file that is built when when the rule's command is executed. For example, in the following rule:

```makefile
intmath.o: intmath.c intmath.h
  gcc217 -c intmath.c
```

The target is `intmath.o`, which is built when the command `gcc217 -c intmath.c` is executed. Recall that this command will be executed if either `intmath.o` does not exist or if one of its dependencies have a more recent modification timestamp.

A flexible feature of `make` is that it does not require that the target actually represent a file. Instead, it can represent a label for an arbitrary command or action you want `make` to execute. Such a target is called a _phony target_. Consider the following rule:

```makefile
hello: 
    echo "Hello, world!" 
```

The target, `hello`, does not represent a file—that is, there is no file in our directory named `hello`, and the command `echo "hello, world"` does not create such a file. (Also notice that the target does not have any dependencies. This is perfectly valid, as dependencies are optional.) What happens when we invoke this rule? Let's give it a shot:

```bash
$ make hello
echo "Hello, world!"
Hello, world!
$
```

We see that `make` executes the command `echo "Hello, world!"`, printing `Hello, world!` on stdout. `make` does not complain about the fact that a file named `hello` was not created by this command.

Here's how it works. When `make` processes this rule, it assumes that `hello` represents a file. It thus looks for a file named `hello` in the working directory. Because it does not find one, it determines that `hello` needs to be built, and it thus executes the command `echo "Hello, world!"`. At this point, `make` considers its job complete. It does not care whether `hello` is in fact created.

The important thing to recognize is that because this rule will never create a file named `hello`, we can run `make hello` as many times as we'd like, and, each time, `make` will execute the command `echo "Hello, world!"`. For example, if we run `make hello` three times in a row:

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

#### Common Phony Targets

In real world makefiles, you'll commonly see the following three phony targets: `all`, `clean`, and `clobber`. Let's enhance our Makefile by adding these three phony targets. An explanation of each is provided below. Note that in a Makefile, everything following `#` on a line is a comment.

{% code title="makefile version 2" %}
```makefile
# Dependency rules for non-file targets

# Default target. Builds entire program. 
all: testintmath

# Delete Emacs backup and autosave files (*~ specifie all files that end with a '~',
# \#*\# specifies all files that start and end with a '#')
clobber: clean
  rm -f *~ \#*\#
  
# Delete all files generated when program is built (i.e., testintmath and .o files)
clean:
  rm -f testintmath *.o
  
  
# Dependency rules for file targets
testintmath: testintmath.o intmath.o
  gcc217 testintmath.o intmath.o –o testintmath
testintmath.o: testintmath.c intmath.h
  gcc217 -c testintmath.c
intmath.o: intmath.c intmath.h
  gcc217 -c intmath.c
```
{% endcode %}

Here's what each of the three phony targets do:

* `all`. To control the default behavior you run make without specifying a target.
* `clean`. to delete the files typically created when the program is built.&#x20;
* `clobber` to extend `clean` by also deleting files like Emacs backup and autosave files.

{% hint style="info" %}
**Purpose of the 'all' target**

You might be wondering what purpose the `all` target serves in our program, as it seems to change nothing about how we build our program. Truthfully, in our program it doesn't serve any real purpose, except perhaps for accommodating users who invoke `make all` out of habit.

The real purpose of `all` is when you have multiple independent targets and them all to be built by default when you invoke `make`. For example, suppose we have a project with two executables:`hello1` and `hello2`. We can set up our makefile as shown below and build both executables by invoking `make`. Without `all`, by default only `hello1` would be built when we invoke `make` . To build both `hello1` and `hello2`, we'd have to explicitly mention both (e.g., by invoking `make hello1 hello2`).

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
