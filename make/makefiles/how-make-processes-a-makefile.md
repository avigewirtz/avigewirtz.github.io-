# How make processes a makefile

make processes our makefile using depth first search. It starts from the default rule and recursively examines all other rules. We'll examine at three different points in development.&#x20;

## Case 1: Building testintmath for the first time

Here's how it works:

* Examines first target, which is testintmath. make notes that it does not exist. It might seem that make should invoke the command to build testintmath now, but that is not the case. Make must first ensure that testintmath's dependencies (intmath.o and testintmath.o) are up to date. In our case, they don't even exist yet.&#x20;
  * Examines testintmath.o. Notes that it does not exist.&#x20;
    *



<figure><img src="../../.gitbook/assets/Group 66 (5).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Note that the graph shown here is essentially identical to the one we've shown all along, except that the direction of the arrows is flipped. Here, an arrow from A to B indicates that A depends on B. Functionally the dependency graphs are identical; the only difference is notation. This notation is more convinient&#x20;
{% endhint %}

When all files are up to date:

<figure><img src="../../.gitbook/assets/Group 67 (1).png" alt=""><figcaption></figcaption></figure>

after modifying intmath.c:

<figure><img src="../../.gitbook/assets/Group 68 (2).png" alt=""><figcaption></figcaption></figure>

## other points i want to make

* A rule can have multiple commands and targets. We won't cover such rules here.&#x20;
* The order in which rules appear in the makefile isn't signifigant, except for the first rule, which&#x20;
* doesn't process all rules. only ones&#x20;
