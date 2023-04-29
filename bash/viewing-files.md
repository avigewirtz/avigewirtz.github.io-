# Viewing Files

File viewing and editing are very different operations. The programs presented in this section are for file viewing only. To edit files, you must use a text editor, such as Emacs, which we’ll cover in a later chapter. &#x20;

## Displaying files

### Syntax: <mark style="color:red;">`cat`</mark> <mark style="color:green;">`OPTION(S)`</mark>` `<mark style="color:blue;">`FILE(S)`</mark>&#x20;

Common options:

* &#x20;**`-n`**   —   Number all output lines.
* &#x20;**`-s`**   —   Squeeze consecutive blank lines into a single blank line.

Examples:

1. Print berra\_qoute.txt on stdout:&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 4.48.26 PM.png" alt=""><figcaption></figcaption></figure>

2. Concatenate berra\_quote.txt and einstein\_quote.txt and print the result on stdout with line numbers:&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 4.48.33 PM.png" alt=""><figcaption></figcaption></figure>

5. Print encyclopaedia.txt on stdout; number all lines and suppress repeated empty lines:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 4.49.17 PM.png" alt=""><figcaption></figcaption></figure>

The entire file will be printed on stdout. Because the file is extremely large (almost 100,000 lines!), this operation will take quite some time, and your terminal will be unusable until it is complete. Once the printing is finally complete, the final page of the file will be displayed: &#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 4.49.28 PM.png" alt=""><figcaption></figcaption></figure>

Cat does not have any useful features for navigating the file’s output; the only way you can navigate the file is by scrolling up and down.&#x20;

As this example demonstrates, cat has a couple of drawbacks particularly for large files. First, all output is immediately printed, and your terminal is unusable until the printing is complete. Second, there is no user-friendly way to navigate through the output.&#x20;

To address these shortcomings, less was created. Less is a terminal pager; that is, a program that displays text files one screenful (page) at a time. Displaying one page at a time has advantages since (1) your terminal screen isn’t cluttered, and (2) it is faster (since the entire file need not be printed before you can access it).

Less also contains many useful features that cat lacks, such as file navigation, searching, and highlighting.&#x20;

## Printing files to stdout one page at a time

### Syntax: <mark style="color:red;">`less`</mark> <mark style="color:green;">`OPTION(S)`</mark> <mark style="color:blue;">`FILE(S)`</mark>&#x20;

Description: Prints file(s) to stdout one screenful (page) at a time. Less contains many useful features, such as searching, highlighting, and backward movement.&#x20;

### Common options

* &#x20;**`-m`**     —   Display the percentage of your position in the file.
* &#x20;**`-n`**     —   Number output lines.
* &#x20;**`-s`**     —   Squeeze consecutive blank lines into a single blank line.
* &#x20;**`-x`**     —   Squeezes consecutive blank lines into a single blank line.

### Examples

1. Print encyclopaedia.txt on stdout one page at a time. Suppress repeated blank lines, add line numbers, and display the percentage of the file displayed so far:  \


<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 4.49.44 PM.png" alt=""><figcaption></figcaption></figure>

The following page will be displayed on stdout:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 4.49.52 PM.png" alt=""><figcaption></figcaption></figure>

### Navigating `less`

| Command               | Effect                                     |
| --------------------- | ------------------------------------------ |
| q                     | Quit                                       |
| h                     | Display a list of commands                 |
| UP-ARROW / DOWN-ARROW | Navigate up and down the file              |
| SPACEBAR              | Go forward one page                        |
| b                     | Go backward one page                       |
| G                     | Go to end of file                          |
| g                     | Go to beginning of file                    |
| /pattern              | Search for text matching “pattern” in file |
