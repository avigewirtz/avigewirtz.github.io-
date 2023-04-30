# Filesystem Layout

The Linux filesystem is organized as a _single_ hierarchical structure, resembling an inverted tree, as shown in **Figure 1**.&#x20;

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption><p>Figure 1: Filesystem Structure</p></figcaption></figure>

\
The top-most directory in the hierarchy structure is conventionally referred to as _root_ and denoted by the / (forward slash) character, though it actually has no name--its "name" is the “empty” part before the / delimiter. Like a tree, the hierarchy “grows” from the root, with paths connecting the root to each of the tree’s directories and files. Each directory may have an arbitrary amount of subdirectories, expanding the structure as necessary. The terms _parent_ and _child_ are commonly used to describe the relationship between a directory and its immediate subdirectory (with the latter being the _child_). In the above snapshot, the directory _tal5_ is a child of _u_ (and _u_ is the parent of _tal5_, _bwk_, and _sgewirtz_).&#x20;

{% hint style="info" %}
This Linux filesystem organizational structure, in which all files and directories, including those from external storage devices like USB drives, descend from the root directory differs from that of Windows. In Windows, the filesystem consists of multiple hierarchies, each represented by a drive letter (e.g., C:, D:, etc.). Each of these drives has its own root directory.
{% endhint %}
