# How 3-way merges work



<figure><img src="../../.gitbook/assets/Group 369.png" alt="" width="563"><figcaption></figcaption></figure>



Assuming the merge is succesful, the result will be a new commit--C7--which master will point to.&#x20;

<figure><img src="../../.gitbook/assets/Group 370.png" alt="" width="563"><figcaption></figcaption></figure>

If there is a conflict, a new commit will not be created. Instead, the merged parts will be in the index/working directory



## Easy case: agreement

agreement between C5 and C6 for file A. For example, file A in C5 and C6 contains word "hello". In this case, it should be fairly obvious that file A containing hello should be included in C7. Git does not even have to check common ancestor, since it would not matter if file A was different in C3 or didnt even exist.&#x20;

<figure><img src="../../.gitbook/assets/Group 373.png" alt="" width="375"><figcaption></figcaption></figure>



## Scenario 2: content different

The second case is where there are disagreements between C5 and C6.&#x20;

Two cases:

1. File A exists in C5 but not C6, or vice versa.&#x20;
2. Content of file A in C5 and C6 different

Let's consider case 1:

* file A exists in C5 or C6 but not in other two: included in C7
* File A unmodified in one and deleted in other. Deleted state reflected in C7.
* File A modified in C5 or C6 and deleted in other. Conflict.&#x20;

<figure><img src="../../.gitbook/assets/Group 388.png" alt="" width="563"><figcaption></figcaption></figure>



Let's now consider case 2, where file A exists in both C5 and C6, but content is different.&#x20;

* File A modified in one and unmodified in other. Modified version included in C7.
* File A modified in both, but separate units modified. Merge of both versions included in C7.
* File A modified in both and modifications conflict. Conflict.
* File A new in both and content not identical. Conflict.&#x20;



<figure><img src="../../.gitbook/assets/Group 387 (1).png" alt="" width="563"><figcaption></figcaption></figure>



## Determining conflict within file



<figure><img src="../../.gitbook/assets/Group 398.png" alt=""><figcaption></figcaption></figure>



* takes the three version of file. find LCS.&#x20;
* All&#x20;









