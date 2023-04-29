# Filenames

Every file has a **filename**. (In this context, the term _file_ is used broadly to include directories—which are a special type of file.) On Linux, filenames are case-sensitive; that is, `hello.c`, `Hello.c` and `HELLO.C` refer to three distinct files.&#x20;

Very few restrictions are placed on filenames. On armlab, which uses the popular Ext4 filesystem, only the following restrictions are imposed:&#x20;

* No two filenames in the same directory may be the same.&#x20;
* Filenames may not exceed 255 bytes. (This normally corresponds to 255 characters.)&#x20;
* Filenames may not contain the `/` (forward slash) or ASCII `NUL` character. (In practice you need not be concerned about NUL. It is included here only for completeness.)

While any filename adhering to these rules is considered valid, some filenames are not ideal for use in a shell environment and are best avoided, as we'll discuss [later](../../bash/creating-files-and-directories.md#directory-and-file-creation).

### Filename extensions&#x20;

A filename extension is a suffix added to the end of a filename, separated by a dot, that usually indicates the format or type of the file. It is usually composed of three or four letters, but it can also be longer. For example, in the filename "document.txt", the extension is ".txt", which indicates that the file is a text file. Other common extensions include ".jpg" for image files, ".mp3" for audio files, and ".pdf" for document files.&#x20;

Filename extensions are not a feature of Linux filesystems; therefore, from Linux’s point of view, they are completely optional and treated like ordinary filename characters. Some programs, however, require input files to have filename extensions, as they rely on them to determine the file type or to enforce specific conventions. For example, the GCC compiler will not compile a C program unless it has a `.c` extension.&#x20;

Using filename extensions is generally considered good practice because it helps users and software easily recognize and understand the contents or format of a file.
