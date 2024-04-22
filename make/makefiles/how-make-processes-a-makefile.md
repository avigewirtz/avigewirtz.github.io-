# How make processes a makefile

### Our makefile in Action

Let's now examine how make processes our makefile. Let's assume we're building testintmath for the first time. Thus, testintmath.o, intmath.o, and testintmath do not currently exist.&#x20;

To run our makefile, we simply invoke make on the command line:

```
make
```

make will search our directory for a file named makefile and begin from the first rule--in our case, the rule for testintmath.&#x20;

<figure><img src="../../.gitbook/assets/Group 66 (5).png" alt=""><figcaption></figcaption></figure>

When all files are up to date:

<figure><img src="../../.gitbook/assets/Group 67 (1).png" alt=""><figcaption></figcaption></figure>

after modifying intmath.c:

<figure><img src="../../.gitbook/assets/Group 68 (2).png" alt=""><figcaption></figcaption></figure>

## other points i want to make

* A rule can have multiple commands and targets. We won't cover such rules here.&#x20;
* The order in which rules appear in the makefile isn't signifigant, except for the first rule, which&#x20;
* doesn't process all rules. only ones&#x20;
