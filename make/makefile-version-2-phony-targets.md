# Phony targets

Make's job is to bring targets up-to-date. Until now, we've assumed that targets represent files, which are brought up-to-date by creating them or updating them. In fact, however, targets need not represent files. They can represent labels for arbitrary commands or actions you want make to execute. Such targets are known as _phony_ targets. 

The mechanism by which make implements phony targets is quite simple. After a rule is processed, make has no postcondition check to verify that the target "file" was in fact build. Instead, it operates under the assumption that if a target's dependencies are satisfied and its commands are successfuly run, the target is up-to-date. As we'll see, a target need not even have any corresponding dependencies or commands, so in the most trivial case, a out-of-date target can be considered brought "up-to-date" even if no work was actaully done. 

Phony targets have two canonical use cases:

* As a label for one or more arbitrary commands you want make to execute. 
* As an alias for one or more other targets, such that running the phony target is the same as running the target(s) directly. 

&#x20;Let's explore both use cases. Suppose we want to use make to automate the task of deleting all files normally created by buildimg our program—that is, the object files and the executable. To achieve this, we can add the following rule to our makefile:&#x20;

```
clean: 
    rm -f *.o testintmath 
```

In this rule, the target is clean, which does not correspond to a file in our project directory, and we give it the command rm -f .o testintmath, which, when run, has the effect of deleting testintmwrh and all objevt files in tje working directiry. When we invoke make clean, the effect is that the command rm -f *.o testintmath gets executed:&#x20;

```
$ make clean
rm -f *.o testintmath 
$
```

Here's how it works. Like any other rule, `make` checks if a file named `clean` exists in the working directory. Since there is no such file, `make` determines that `clean` needs to be built. In an attempt to build `clean`, `make` executes the command rm -f testintmath \*.o. Because this command runs successfuly(that it, returns exit status 0), make considers clean up-to-date (for the current invocation of make, that is). It does not actaully verify that clean is created.&#x20;

We can see this full sequence of operations by invoking make clean with the debug=-v option.&#x20;
This prints out 

Importantly, notice the last line where it says ``Successfully remade target file `run'.``&#x20;



















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
