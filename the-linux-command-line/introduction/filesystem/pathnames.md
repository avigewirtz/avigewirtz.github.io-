# Pathnames

Every file and directory has a _pathname_, which is a string that uniquely identifies its location in the directory hierarchy. There are two types of pathnames: _absolute_ or _relative_. An absolute pathname pinpoints the location of a file or directory by specifying its path from the root directory; a relative pathname specifying its path from the working directory.&#x20;

### Absolute pathnames

The absolute pathname of a directory or file has the following format:

```
/dir1/dir2/…/dirN_or_file
```

The first _/_ represents the root directory; the intermediate directories, each delimited by _/_, represent the directories on the trail from the root directory to _dirN\_or\_file_. Figure 3 illustrates four absolute pathnames.

<figure><img src="https://lh6.googleusercontent.com/L5AY4VGHdsVYWSKkicK4tU758bIXimYQphD7_ojQwtjKISL6dhGrPlLbFVKurw_vqRGYRbmp4ZTV22RP9QmeL9oNkaf83SRzdP0Ou6oJ7Akomg2DbQrtY7iJa-lKHdbh39qvpm0cceJBFW54y499qbQ" alt=""><figcaption><p>Figure 3: Absolute Pathname Examples</p></figcaption></figure>

### Relative pathnames

The relative pathname of a directory or file has the following format:

```
dir1/dir2/…/dirN_or_file
```

_dir1_ normally represents the parent (denoted `..`) or child of the working directory, but it can also represent the working directory itself (denoted `.`). The intermediate directories, each delimited by _/_, represent the directories on the trail from _dir1_ to _dirN\_or\_file_. Figure 4 illustrates four relative pathnames.

<figure><img src="https://lh3.googleusercontent.com/G6fYIoWumsNAoXkf7lnMwc5TEdyJ1zDcFSyqwmyFm-J8xG0YwJB2-zCmzuwDkOFFEv-Tzo3l8e7e7h9KkrJbfBO7qe7Khj5caDlE8P8R_kN2H8RAA_LF2gD-uk5dSEQK23Yv1DxJM0F4chlgWH3tnYE" alt=""><figcaption><p>Figure 4: Relative Pathname Examples</p></figcaption></figure>

It's important to note that the working directory can change during a session, so the meaning of a relative pathname is context specific.&#x20;
