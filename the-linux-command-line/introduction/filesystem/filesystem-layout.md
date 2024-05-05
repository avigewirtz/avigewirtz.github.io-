# Directory Hierarchy

The fact that a directory can contain other directories leads to a hierarchical filesystem structure, resembling an inverted tree. Figure 1 shows part of a typical directory hierarchy.&#x20;

<figure><img src="../../../.gitbook/assets/filesystem10.17 (16).png" alt=""><figcaption></figcaption></figure>

The top-most directory is conventionally referred to as the _root directory_ and denoted by the `/` (forward slash) character, though it technically has no name--its "name" is the “empty” part before the `/`. Unlike some other filesystems, which have multiple root directories, Linux has a single root directory. Like a tree, the hierarchy grows from the root, with paths connecting the root to each of the tree’s subdirectories and files. Each directory may have an arbitrary amount of subdirectories, expanding the structure as necessary. The terms _parent_ and _child_ are commonly used to describe the relationship between two adjacent directories. In the above snapshot, for example, `u` is the parent of `tal5`, `bwk`, and `sgewirtz`, and they are `u`'s children.

{% hint style="info" %}
To avoid having to always say "files and directories", will often refer to them as just files. This is techincally correct, since directory is a type of file. When there is a clear distinction
{% endhint %}



{% hint style="info" %}
Important standard directories

Every Linux filesystem has a set of important directories residing in the root directory. These directories are essential for the proper functioning of the system, and the presence of most of them is required by the [Filesystem Hierarchy Standard](https://refspecs.linuxfoundation.org/FHS\_3.0/fhs/index.html) (FHS). Here is a very brief overview of many of these directories:&#x20;
{% endhint %}
