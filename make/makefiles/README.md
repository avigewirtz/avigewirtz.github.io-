# Makefiles

To use Make, you create a file in your project directory called a makefile, which tells make how to build your program. You can name this file _makefile_ or _Makefile_ (or even _GNUMakefile_, if you're using GNU Make). GNU recommends naming it Makefile.&#x20;

A makefile primarily consists of _rules_, which typically have the following syntax:&#x20;

```
target: dependencies
<tab> command
```

where target

Let's demonstrate how this works in practice by means of a simple example:

```
hello: hello.c
    gcc hello.c -o hello
```

hello is the target, which needs to be built if either it does not exist, or if it does exist but is older than hello.c.&#x20;



{% hint style="danger" %}
One of the most common errors in writing Makefiles is using spaces (ASCII character 32) before the command instead of a tab (ASCII character 9). This can also happen when editing a Makefile in a text editor that automatically converts tabs to spaces. This will lead to the following error:

```
   *** missing separator.  Stop.
```
{% endhint %}



























Here’s a simple makefile for our testintmath program:

{% code title="makefile " lineNumbers="true" %}
```makefile
testintmath: testintmath.o intmath.o
  gcc testintmath.o intmath.o –o testintmath
  
testintmath.o: testintmath.c intmath.h
  gcc -c testintmath.c
  
intmath.o: intmath.c intmath.h
  gcc -c intmath.c
```
{% endcode %}

## Running makefile

* invoke make by typing make TARGET
* if target is ommited, will defualt to first target





### makefile in Action

Let's examines what happens the first time we invoke the makefilefirst time



Invoking make again:

modifying intmath.c and invoking make:



## other points i want to make:

* comments&#x20;
* rule can have multiple commands and can have more than one target. won't cover that here
* makefile names&#x20;

