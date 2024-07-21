# Phony targets

Make's job is to bring targets up-to-date. Until now, we've assumed that targets represent files, which are brought up-to-date by creating them or updating them. In fact, however, targets need not represent files. They can represent labels for arbitrary commands or actions you want make to execute. Such targets are known as _phony_ targets.

`make` implements phony targets in quite a simple manner. After a rule is processed, `make` has no postcondition check to verify that the target "file" was in fact built. Instead, it operates under the assumption that if a target's dependencies (if any) are satisfied and its commands (if any) are successfully run, the target is up-to-date. Phony targets have two canonical use cases:

* As a label for one or more arbitrary commands you want make to execute.
* As an alias for one or more other targets, such that running the phony target is the same as running the target(s) directly.

In this section, we'll explore both use cases. Take a look at Makefile version 2, shown below, which contains three commonly used phony targets: `all`, `clean`, and `clobber`. Don't worry for now how they work. We'll go over each one by one.

{% code title="makefile version 2" %}
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
  =
intmath.o: intmath.c intmath.h
  gcc -c intmath.c
```
{% endcode %}

#### `clean`

Consider the `clean` rule:

```
clean: 
    rm -f *.o testintmath 
```

The target, `clean`, does not represent a file—that is, there is no file in our project directory named `clean`, and the command `rm -f *.o testintmath` does not create such a file. Nevertheless, we can run this rule, and the effect is that `rm -f *.o testintmath` will be executed:

```bash
$ make clean
rm -f *.o testintmath 
$
```

This command deletes the executable `testintmath` as well as all files with a `.o` extension (i.e., `testintmath.o` and `intmath.o`), thereby "cleaning" our project directory. This is useful in situations where we want to rebuild `testintmath` from scratch. Note that the name `clean` isn't special. We could have named the rule anything we want, such as `delete_build_files`. `Clean` is just the conventional name for this kind of task in Makefiles.

Here's how make processes this rule. As with any other rule, `make` begins by checking if a file named `clean` exists in the working directory. Since there is no such file, `make` determines that `clean` needs to be built. In an attempt to build `clean`, `make` executes the command `rm -f testintmath *.o`. Because this command runs successfully (that it, returns exit status 0), `make` considers `clean` up-to-date (for the current invocation of `make`, that is). It does not actually verify whether `clean` is created.

You can see this full sequence of operations by invoking `make clean` with the `debug=-v` option. The output should look like this:

```
$ make clean --debug=v
GNU Make 3.81
Copyright (C) 2006  Free Software Foundation, Inc.
This is free software; see the source for copying conditions.
There is NO warranty; not even for MERCHANTABILITY or FITNESS FOR A
PARTICULAR PURPOSE.

This program built for i386-apple-darwin11.3.0
Reading makefiles...
Reading makefile `makefile'...
Updating goal targets....
Considering target file `clean'.
 File `clean' does not exist.
 Finished prerequisites of target file `clean'.
Must remake target `clean'.
rm -f testintmath *.o
Successfully remade target file `clean'.
$ 
```

Notice how after executing the command `rm -f testintmath *.o`, make reports that it ``Successfully remade target file `clean'``. Of course, a file named `clean` was not in fact created, but make&#x20;

An important aspect to recognize is that because this rule will never create a file named `clean`, `clean` will always be considered out of date. Therefore, its command will be run each time we invoke `make clean`:

```bash
$ make clean
rm -f *.o testintmath 
$ make clean
rm -f *.o testintmath 
$ make clean
rm -f *.o testintmath 
$
```

{% hint style="warning" %}
**.PHONY Directive**

It should go without saying that the scheme we just described will only work if there is in fact no file named `clean` in the working directory. If there is such a file, running `make clean` will always yield:

```makefile
$ make clean
make: `clean' is up to date.
$
```

GNU Make offers a simple solution to this potential issue. Just declare `clean` as phony, like so:

```makefile
.PHONY: clean
clean: 
    rm -f *.o testintmath 
```

With this declaration, this rule will work as intended even if there is a file named `clean` in the working directory.
{% endhint %}

#### `clobber`

Consider the `clobber` rule:

```
clobber: clean
  rm -f *~ \#*\# 
```

This rule is designed to extend the `clean` rule by not only removing the build artifacts but also other temporary or backup files that might clutter the project directory. When you run:

```
$ make clobber
rm -f testintmath *.o
rm -f *~ \#*\# 
$ 
```

Here's how it works. make first checks if a file named `clobber` exists in the working directory. Since there is no such file, make determines that `clobber` is out-of-date and needs to be built. Before make can "build" clobber, however, it must first ensure that its dependency, clean, is up-to-date. So make moves on to clean. make sees that clean doesn't exist, so it executes the command rm -f testintmath \*.o in an attempt to build it. Since this command executes successfully, make considers clean up-to-date (for the current invocation of make, that is). Make then go back to clobber and runs the command rm -f \*\~ \\#\*\\# . This command has the effect of deleting Emacs backup files.

`make` first executes the `clean` rule, ensuring that all `.o` files and the `testintmath` executable are deleted. After successfully running the `clean` rule, `make` proceeds to execute the command `rm -f *~ \#*\#`. This command deletes all files ending in `~` (typically backup files created by text editors) and files with names matching the pattern `#*#` (common for temporary or autosave files).

#### `all`

Consider the `all` rule:

```makefile
all: testintmath
```

`make` then checks if `testintmath` is up-to-date. If `testintmath` is not present or any of its dependencies are newer than the `testintmath` executable, `make` proceeds to build `testintmath`.. all does not represent a file, and this rule has no command. The affect of running this rule is that make ; hiwever, unlike coean and cllbber, it has no corresponding command. Instead, it essentially serves as an alias for testintmath, meaning that the affect of running make all is the same as running make testintmath. If we run all, the





































{% hint style="info" %}
**Purpose of the 'all' target**

You might be wondering what purpose the `all` target serves in our program compared to simply using `testintmath` as the default target. Truthfully, it doesn't serve any real purpose, except perhaps for accommodating users who might invoke `make all` out of habit.

The real purpose of `all` is to group multiple independent targets and effectively make them all default targets. For example, suppose we have a project with two executables:`hello1` and `hello2`. Making `hello1` and `hello2` dependencies of `all` effectively makes them both default targets (which will be triggered when we run `make`).

```makefile
all: hello1 hello2

hello1: hello1.c
	gcc -c hello1.c

hello2: hello2.c
	gcc -c hello2.c
```
{% endhint %}
