# Filenames

A few points on filenames in Linux are worthy of mention:

* Linux places very few restrictions on filenames. No two filenames in the same directory may be the same, and filenames may not contain the  `/` and _ASCII NUL_ characters_._&#x20;
* Filenames are case-sensitive; that is, _hello.c_, _Hello.c_ and _HELLO.C_ refer to three distinct files.&#x20;
* Linux has no concept of filename extension. They are entirely optional and treated as ordinary filename characters. In other words,&#x20;
* Files whose names begin with a  `.`  (e.g., `.bashrc`) are _hidden_, meaning that by default they are not displayed in directory listings--whether in a GUI or CLI environment. We'll go over how to display them in our coverage of the [`ls`](../../navigating-the-filesystem/#ls-a-sense-of-surroundings) command.&#x20;
