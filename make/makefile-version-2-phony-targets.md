# Phony targets

Make's job is to bring targets up-to-date. We've assumed that targets represent files, which are brought up-to-date by creating them or rebuilding them. In fact, however, targets need not represent files. Instead, they can represent labels for arbitrary commands or actions you want make to execute. Such targets are known as _phony_ targets. 

The mechanism by which make implements phony targets is very simple. After a rule is processed, make has no postcondition check to verify that the target "file" was in fact build. Instead, it operates under the assumption that if a target's dependencies are satisfied and its commands are successfuly run, the target is up-to-date. As we'll see, a target need not even have any corresponding dependencies or commands, so in the most trivial case, a out-of-date target can be considered brought "up-to-date" even if no work was actaully done. 

Phony targets have two canonical use cases:

* As a label for one or more arbitrary commands you want make to run. 
* As an alias for one or more other targets, such that running the phony target is the same as running the other target(s) directly. 

&#x20;Let's explore both use cases. Suppose we want to use make to automate the task of running our testintath. In other words, to execute the command `./testintmath`. To achieve this, we can add the following rule to our makefile:&#x20;

```
run: testintmath
    ./testintmath
```

In this rule, we name the target run, which does not correspond to a file in the working directory, and we provide the command `./testintmath`. Additionally, we list `testintmath` as a dependency, ensuring that `testintmath` is up-to-date before it's run. \
\
When we invoke make run, the effect is that our program is run:&#x20;

```
$ make run
./testintmath
Enter the first positive integer:
2
Enter the second positive integer:
3
The greatest common divisor of 2 and 3 is 1.
The least common multiple of 2 and 3 is 6.
$
```

Here's how it works. Like with any other target, make checks if a file named run exists in the working directory. Because it does not make determines that `run` needs to be "built". Before doing so, however, it must first ensure that run's dependency, testintmath, is up-to-date. It therefore processes the rule for testintmath, bringing testintmath up-to-date, if need be. With the dependency check satisfied, it then runs ./testintmath in an attempt to build the target run. because this command Of course, this command does not actaully build run, but this does not cause an error, This command does not actaully build run, but make has no postcondition check to verify that run is actaully built. So long as the command runs successfuly (that it, returns exit status 0) make considers run as being succesffuly brought up-to-date (for the current invocation of make, that is).&#x20;

We can see this full sequence of operations by invoking make run with the debug=-v option.&#x20;

```
~/hello> make run --debug=v
GNU Make 3.81
Copyright (C) 2006  Free Software Foundation, Inc.
This is free software; see the source for copying conditions.
There is NO warranty; not even for MERCHANTABILITY or FITNESS FOR A
PARTICULAR PURPOSE.

This program built for i386-apple-darwin11.3.0
Reading makefiles...
Reading makefile `makefile'...
Updating goal targets....
Considering target file `run'.
 File `run' does not exist.
  Considering target file `testintmath'.
    Considering target file `testintmath.o'.
      Considering target file `testintmath.c'.
       Finished prerequisites of target file `testintmath.c'.
      No need to remake target `testintmath.c'.
      Considering target file `intmath.h'.
       Finished prerequisites of target file `intmath.h'.
      No need to remake target `intmath.h'.
     Finished prerequisites of target file `testintmath.o'.
     Prerequisite `testintmath.c' is older than target `testintmath.o'.
     Prerequisite `intmath.h' is older than target `testintmath.o'.
    No need to remake target `testintmath.o'.
    Considering target file `intmath.o'.
      Considering target file `intmath.c'.
       Finished prerequisites of target file `intmath.c'.
      No need to remake target `intmath.c'.
      Pruning file `intmath.h'.
     Finished prerequisites of target file `intmath.o'.
     Prerequisite `intmath.c' is older than target `intmath.o'.
     Prerequisite `intmath.h' is older than target `intmath.o'.
    No need to remake target `intmath.o'.
   Finished prerequisites of target file `testintmath'.
   Prerequisite `testintmath.o' is older than target `testintmath'.
   Prerequisite `intmath.o' is older than target `testintmath'.
  No need to remake target `testintmath'.
 Finished prerequisites of target file `run'.
Must remake target `run'.
./testintmath
Enter the first positive integer:
3
Enter the second positive integer:
2
The greatest common divisor of 3 and 2 is 1.
The least common multiple of 3 and 2 is 6.
Successfully remade target file `run'.
~/hello> 
```

Importantly, notice the last line where it says ``Successfully remade target file `run'.``&#x20;



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
