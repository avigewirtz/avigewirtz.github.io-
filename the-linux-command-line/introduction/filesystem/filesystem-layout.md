# Directory Hierarchy

The Linux filesystem is organized as a single hierarchical structure, resembling an inverted tree. At the base is the _root directory_, denoted by `/` (slash), from which all files and directories in the system descend. An example of this hierarchical structure is shown in Figure 1, which depicts a partial snapshot of the Armlab filesystem.

<figure><img src="../../../.gitbook/assets/image (3) (1).png" alt=""><figcaption><p>Figure 1: Filesystem Structure</p></figcaption></figure>

{% hint style="info" %}
The terms _parent_ and _child_ are commonly used to describe the relationship between a adjacent directories. In the above snapshot, for example, `tal5` is a child of `u` (and `u` is the parent of `tal5`, `bwk`, and `sgewirtz`).
{% endhint %}
