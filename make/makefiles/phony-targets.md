# Phony targets

In a makefile, a rule's target typically represents the name of a file that is to be built by the rule's command. For example, in the following rule:

```
intmath.o: intmath.c intmath.h
  gcc217 -c intmath.c
```

the target is intmath.o, which represents a file that is built when the command `gcc217 -c intmath.c` is executed.&#x20;

An interesting feature of make is that a rule's command need not actually create the target file--in fact, the target need not represent a file at all. Instead, it can serve as a label for a command you want make to execute. Such a target is called a _phony target_. For example, we can create the following rule:

```
sayHello:
    echo "Hello there!" 
```

The target `sayHello` is a phony target, since the command `echo "Hello there!"` doesn't lead to the creation of a file named `sayHello`. Instead, its sole purpose is to enable you to execute the `echo "Hello there!"` command via the makefile. In other words, invoking `make sayHello` causes "Hello there!" to be printed on stdout:

```
$ make sayHello
echo "Hello there!"
Hello there!
```

Couple of notes regarding phony targets:

* don't make them first rule
* Not intended to match a filename in your directory.&#x20;

## Common phony targets

Common phony targets you'll encounter in makefiles There are three phony targets that are common in makefiles: all, clean, and clobber.&#x20;

#### Clean

clean is used to delete the files that were generated during the build process. It's a way to "clean up" your project directory, so you can start a fresh build.

```
clean:
  rm -f testintmath *.o
```

`rm -f testintmath *.o` removes _testintmath_ as well as all files in the current directory with the _.o_ extension.

#### Clobber

The `clobber` rule is typically used to extend the functionality of the `clean` rule. It not only removes the files generated during the build process (as done by the `clean` rule) but also gets rid of backup and temporary files that are often created by text editors or development environments.

```
clobber: clean
    rm -f *~ \#*\#
```

`*~`:  Specifies all files in the current directory that end with a \~ (i.e., `example.c~`), and `\#*\#` specifies all files in the current directory that start and end with # (i.e.,`#example.c#`). These files are Emacs backup and autosave files.

#### All

If you have multiple independent targets you want to run via a single invocation of make, you can do so by making them all a dependency of a single target. Standard practice is to call such a target all. For example, suppose we have two executables: hello1 and hello2.&#x20;

```
all: hello1 hello2

hello1: hello1.0
	gcc hello1.o -o hello1
	
hello2: hello2.0
	gcc hello2.o -o hello2

hello1.o: hello1.c
	gcc -c hello1.c

hello2.o: hello2.c
	gcc -c hello2.c
```

## makefile version 2

{% code title="makefile version 2" %}
```makefile
# Dependency rules for non-file targets
all: testintmath
clobber: clean
  rm -f *~ \#*\#
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

A few notes regarding phony targets in our makefile:

* If you want to execute a phony target, you&#x20;
* all phony target doesn't serve any real purpose in our makefile, since
