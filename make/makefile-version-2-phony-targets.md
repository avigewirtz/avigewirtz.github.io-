# Phony targets

Make's job is to bring target files up-to-date. It would seem that make should verify that the target file exists and is newer than all its dependencies. However, that's not actually how make works. It has no postcondition check to verify that the target is in fact built. Instead, it operates under the assumption that is a target's dependencies (if any) are satisfied and its commands (if any) are successfully run, the target is up-to-date. The implication is that a target need not actually be a file. Such targets are called phony targets. Phony targets have two canonical use cases:

* As a label for one or more arbitrary commands you want make to run
* As an alias for one or more other targets, such that running the phony target is the same as running the other targets directly

Let's explore both use cases. Suppose we were to add the following rule to our makefile:

```
clean: 
    rm -f *.o testintmath
```

The target is `objects`, which does not represent a file in our project. It depends on `intmath.o` and `testintmath.o`, and it has no command. It would seem that this rule should produce an error, since&#x20;





`make` assumes that each target represents a file that is built when its corresponding command is run. However, it has no verification mechanism to check whether the target was actually built by the command. Instead, it operates under the assumption that if a target's command is successfully run, the target is up-to-date. This is not a bug in `make` but a deliberate design choice, as it enables the use of so-called _phony_ targets—targets that do not correspond to actual files but represent labels for arbitrary commands or actions you want `make` to execute.

Phony targets are easiest to illustrate by means of an example, so let's jump right into makefile version 2, shown below, which contains three commonly used phony targets: `all`, `clean`, and `clobber`. Don't worry for now how they work for now. We'll go over each one by one.

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
  

objects: testintmath.o intmath.o
  
# Dependency rules for file targets
testintmath: testintmath.o intmath.o
  gcc testintmath.o intmath.o –o testintmath
  
testintmath.o: testintmath.c intmath.h
  gcc -c testintmath.c
  
intmath.o: intmath.c intmath.h
  gcc -c intmath.c
```
{% endcode %}

Let's start with the `clean` rule:

```makefile
clean:
  rm -f testintmath *.o
```

There is no file in our working directory named `clean`, and the command `rm -f testintmath *.o` does not create such a file. Instead, it serves as a label for the command `rm -f testintmath *.o`, meaning that when we run `make clean`, the effect is that `rm -f testintmath *.o` gets executed:&#x20;

```bash
$ make clean
rm -f testintmath *.o
$ 
```

This command deletes `testintmath` as well as all object files (`.o`), effectively "cleaning" the project directory. (Note that the name `clean` isn't special. We could have named the rule anything we want, such as `delete_temp_files`. `Clean` is just the conventional name for this kind of task in Makefiles.)

Here's how it works under the hood. Like any other rule, `make` checks if a file named `clean` exists in the working directory. Since there is no such file, `make` determines that `clean` is out-of-date and needs to be built. In an attempt to build `clean`, `make` executes its corresponding command,  rm -f testintmath \*.o. At this point, make considers clean to be up-to-date. It does not actaully verify that clean is created.&#x20;

Consider the `clobber` rule:

```
clobber: clean
  rm -f *~ \#*\# 
```

clobber is a phony target that depends on another phony target--clean. When we run this rule, the effect is that both rm -f testintmath \*.o and rm -f \*\~ \\#\*\\#  are executed:&#x20;

```
$ make clobber
rm -f testintmath *.o
rm -f *~ \#*\# 
$ 
```

Here's how it works. make first checks if a file named `clobber` exists in the working directory. Since there is no such file, make determines that `clobber` is out-of-date and needs to be built. Before make can "build" clobber, however, it must first ensure that its dependency, clean, is up-to-date. So make moves on to clean. make sees that clean doesn't exist, so it executes the command rm -f testintmath \*.o in an attempt to build it. Since this command executes successfully, make considers clean up-to-date (for the current invocation of make, that is). Make then go back to clobber and runs the command rm -f \*\~ \\#\*\\# . This command has the effect of deleting Emacs backup files.&#x20;

The clean and clobber phony targets demonstrate how phony tatgets enabke us to use make to execute commands that don't incolve building files. Another canocial use case of phony yatgets is to serve as an alias from one or more other garegts such that run the alias is equivelant to running the target(s) directly.  Consider the all phony target:

```makefile
all: testintmath
```

all does not represent a file, and this rule has no command. The affect of running this rule is that make ; hiwever, unlike coean and cllbber, it has no corresponding command. Instead, it essentially serves as an alias for testintmath, meaning that the affect of running make all is the same as running make testintmath. If we run all, the

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

#### .PHONY Directive

It should go without saying that this scheme only works if there is in fact never a file named `hello` in the working directory. If there is such a file, it will always be considered up to date, and running `make hello` will always yield:

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
