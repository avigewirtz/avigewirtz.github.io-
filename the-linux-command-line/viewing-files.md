# Viewing Files

In this section, we'll go over four commands for viewing the contents of files: cat, less, head, and tail.&#x20;

## cat

A quick and easy way to view the contents of a file is with the `cat` command, which prints the contents of a file on the screen. For example, to print berra\_quote.txt, invoke:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 4.48.26 PM.png" alt=""><figcaption></figcaption></figure>

#### Combining contents of multiple files

The name `cat` is short for "concatenate," which may be a hint that it can be used to combine the contents of multiple files. To do so, simply provide both files as arguments to cat:

#### Numbering output lines

**`-n`**: Numbers all output lines.



1. Concatenate _berra\_quote.txt_ and _einstein\_quote.txt_ and display the result on screen with line numbers:&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 4.48.33 PM.png" alt=""><figcaption></figcaption></figure>

## heads and tails

Two complementary commands for inspecting files are `head` and `tail`, which respectively allow us to view the beginning (head) and end (tail) of the file. The `head` command shows the first 10 lines of the file ([Listing 3.2](https://www.learnenough.com/command-line-tutorial/inspecting\_files#code-head)).



While `tail` shows the last 10 lines of the file ([Listing 3.3](https://www.learnenough.com/command-line-tutorial/inspecting\_files#code-tail)).



These two commands are useful when (as is often the case) you know for sure you only need to inspect the beginning or end of a file.



## less

`cat` has two main drawbacks. First, It prints the entire on stdout. This can cause issues when the file is extremely large. For example, say you print a file such as _encyclopaedia.txt_ with cat, which contains almost 100,000 lines of text. Printing all the output takes quite some time, and your terminal will be unusable until it is complete.&#x20;

The second drawback of `cat` is it does not have any useful features for navigating the file’s output; the only way you can navigate the file is by scrolling up and down.&#x20;

To address these shortcomings with `cat`, other tools were developed. A popular alternative is the  `less.`

The `less` program is interactive, so it’s hard to capture in print, but here’s roughly what it looks like:

The advantage of `less` over cat is that it lets you navigate through the file in several useful ways, such as moving one line up or down with the arrow keys, pressing the spacebar to move a page down, and pressing `⌃F` to move forward a page (i.e., the same as spacebar) or `⌃B` to move back a page. To quit `less`, type `q` (for “quit”).

I encourage you to get in the habit of using `less` as your go-to utility for looking at the contents of a file. The skills you develop have other applications as well; for example, the man pages ([Section 1.4](https://www.learnenough.com/command-line-tutorial#sec-man\_pages)) use `less`, so by learning about `less` you’ll get better at navigating the man pages as well.

Perhaps the most powerful aspect of `less` is the forward slash key `/`, which lets you search through the file from beginning to end. For example, suppose we wanted to search through `sonnets.txt` for “rose” ([Figure 3.1](https://www.learnenough.com/command-line-tutorial/inspecting\_files#fig-tudor\_rose)),[6](https://www.learnenough.com/command-line-tutorial/inspecting\_files#cha-3\_footnote-6) one of the most frequently used images in the _Sonnets_.[7](https://www.learnenough.com/command-line-tutorial/inspecting\_files#cha-3\_footnote-7) The way to do this in `less` is to type `/rose` (read “slash rose”), as shown in [Listing 3.6](https://www.learnenough.com/command-line-tutorial/inspecting\_files#code-rose\_search).

The result of pressing return after typing `/rose` in [Listing 3.6](https://www.learnenough.com/command-line-tutorial/inspecting\_files#code-rose\_search) is to highlight the first occurrence of “rose” in the file. You can then press `n` to navigate to the next match, or `N` to navigate to the previous match.



<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 4.49.52 PM.png" alt="" width="563"><figcaption></figcaption></figure>

Table 2 summarizes commonly used less commands.&#x20;

| Command               | Effect                                  |
| --------------------- | --------------------------------------- |
| q                     | Quit                                    |
| h                     | Display a list of commands              |
| UP-ARROW / DOWN-ARROW | Navigate up and down the file           |
| SPACEBAR              | Go forward one page                     |
| b                     | Go backward one page                    |
| G                     | Go to end of file                       |
| g                     | Go to beginning of file                 |
| /pattern              | Search file for text matching “pattern” |
