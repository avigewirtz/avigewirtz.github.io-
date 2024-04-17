# Tags

A tag serves to distinguish a particular commit by giving it a human-readable name in a namespace reserved for this purpose. Otherwise, commits are in a sense anonymous, normally referred to only by their position along some branch, which changes with time as the branch evolves (and may even disappear if the branch is later deleted). The tag content consists of the name of the per‐ son making the tag, a timestamp, a reference to the commit being tagged, and free-form text similar to a commit message.

A tag can have any meaning you like; often, it identifies a partic‐ ular software release, with a name like coolutil-1.0-rc2 and a suitable message. You can cryptographically sign a tag just as you can a commit, in order to verify the tag’s authenticity.

NOTE

There are actually two kinds of tags in Git: “lightweight” and “annotated.” This section refers to annotated tags, which are represented as a separate kind of object in the repository database. A lightweight tag is entirely different; it is simply a name pointing directly to a commit (see the upcoming section on refs to understand how such names work generally).
