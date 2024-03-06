# Compilation Stage

In the second stage of the build process, gcc sends testcircle.i and circle.i to the compiler, which translates testcircle.i and circle.i into assembly language. It's output is stored in testcircle.s and circle.s.&#x20;

Shown in Figure 1.

<figure><img src="../../.gitbook/assets/Group 20 (5).png" alt=""><figcaption></figcaption></figure>



A detailed explanation of assembly language is beyond the scope of this chapter. Can find a high level-overview here, and will be covered in depth later in course.

Assembly language is essentially a human-readable version of the target processor’s machine language.&#x20;

A detailed explanation of of assembly language is beyond the scope of this chapter. Can find a high level-overview here, and will be covered in depth later in course.&#x20;

#### Comparison of C vs Assembly&#x20;

Abstraction Level:

* Specific to target architecture:&#x20;
  * each architecture has it's own assembly lang
  * compiler knows which assembly language to compile to
* Lowest-level human-readable programming language. familiarity with processor's architecture.&#x20;
* Not portable\


ASIDE: why Can’t assembly be converted from one form to another?&#x20;



{% hint style="info" %}
Why can’t assembly be compiled for different architecture
{% endhint %}
