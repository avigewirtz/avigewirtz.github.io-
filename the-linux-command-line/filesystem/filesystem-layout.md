# Filesystem Structure

The Linux filesystem is organized as a hierarchical structure, resembling an inverted tree. Figure 1 shows a (partial) snapshot of the Armlab directory hierarchy.

<figure><img src="../../.gitbook/assets/image (3) (1).png" alt=""><figcaption><p>Figure 1: Filesystem Structure</p></figcaption></figure>

\
The top-most directory is conventionally referred to as the _root directory_ and denoted by the `/` (forward slash) character, though it technically has no name--its "name" is the “empty” part before the `/`. Like a tree, the hierarchy “grows” from the root, with paths connecting the root to each of the tree’s subdirectories and files. Each directory may have an arbitrary amount of subdirectories, expanding the structure as necessary. The terms _parent_ and _child_ are commonly used to describe the relationship between two adjacent directories. In the above snapshot, for example, `u` is the parent of `tal5`, `bwk`, and `sgewirtz`, and they are `u`'s children.

{% hint style="info" %}
This organizational structure, in which all files and directories--including those from external storage devices like USB drives--descend from a single directory differs from the organizational structure found on Windows, where the filesystem is composed of multiple hierarchies, each with their own root directory and represented by a drive letter (e.g., C:, D:, etc.).
{% endhint %}
