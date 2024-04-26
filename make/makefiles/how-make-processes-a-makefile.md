# How make processes a makefile

`make` processes a makefile by doing a depth first search traversal of its dependency graph, starting from the default target. Let's examine three cases for `testintmath`.&#x20;

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
