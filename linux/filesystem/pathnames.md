# Pathnames

Every file and directory has a _pathname_, which is a string that uniquely identifies its location in the directory hierarchy. Pathnames can be categorized into two types: _absolute_ and _relative_. 

Absolute pathnames pinpoint the location of a file or directory by specifying its path from the _root_ directory, whereas relative pathnames pinpoint the location of a file or directory by specifying its path from the _working_ directory.&#x20;

### Absolute pathnames

The absolute pathname of a directory or file has the following format:&#x20;

```
/dir1/dir2/…/dirN_or_file
```

The first _/_ represents the root directory; the intermediate directories, each delimited by _/_, represent the directories on the trail from the root directory to _dirN_or_file_. **Figure 3** shows examples of four absolute pathnames.&#x20;

<figure><img src="https://lh6.googleusercontent.com/L5AY4VGHdsVYWSKkicK4tU758bIXimYQphD7_ojQwtjKISL6dhGrPlLbFVKurw_vqRGYRbmp4ZTV22RP9QmeL9oNkaf83SRzdP0Ou6oJ7Akomg2DbQrtY7iJa-lKHdbh39qvpm0cceJBFW54y499qbQ" alt=""><figcaption><p>Figure 3: Absolute Pathname Examples</p></figcaption></figure>

### Relative pathnames

The relative pathname of `dirN_or_file` has the following format:&#x20;

```
dir1/dir2/…/dirN_or_file
```

`dir1` normally represents the parent or child of the working directory, but it can also represent the working directory itself. The intermediate directories, each delimited by `/`, represent the directories on the trail from `dir1` to `dirN_or_file`. **Figure 4** shows examples of relative pathnames.&#x20;

<figure><img src="https://lh3.googleusercontent.com/G6fYIoWumsNAoXkf7lnMwc5TEdyJ1zDcFSyqwmyFm-J8xG0YwJB2-zCmzuwDkOFFEv-Tzo3l8e7e7h9KkrJbfBO7qe7Khj5caDlE8P8R_kN2H8RAA_LF2gD-uk5dSEQK23Yv1DxJM0F4chlgWH3tnYE" alt=""><figcaption><p>Figure 4: Relative Pathname Examples</p></figcaption></figure>

It's important to note that the working directory can change during a session, so a relative pathname may point to different locations depending on the current working directory.

{% hint style="info" %}
You can determine whether a pathname is absolute or relative by inspection: Absolute pathnames always begin with a / (forward slash); relative pathnames do not.&#x20;
{% endhint %}
