# Viewing Files

There are numerous commands you can use to view the contents of a file. In this section, we'll go over four of them: `cat`, `head`, `tails`, and `less`.&#x20;

## cat

A quick and easy way to view the contents of a file is by using the `cat` command, which displays the file's contents in the terminal window. Its most basic use is to display the contents of a single file. To do this, type `cat` followed by the name of the file you want to view. For example:

```bash
~/CLI_playground$ cat berra_quote.txt
The future ain't what it used to be. - Yogi Berra
~/CLI_playground$
```

If the file is longer than what can be displayed on one screen, the terminal will show the end of the file. To view the beginning, you'll need to scroll all the way up. &#x20;

#### Numbering output lines

You can number the output lines by using the `-n` option. For example:&#x20;

```bash
~/CLI_playground$ cat -n the_odyssey.txt
 ...
 ...
 10415	But Ulysses gave a great cry, and gathering himself together swooped
 10416	down like a soaring eagle. Then the son of Saturn sent a thunderbolt
 10417	of fire that fell just in front of Minerva, so she said to Ulysses,
 10418	"Ulysses, noble son of Laertes, stop this warful strife, or Jove will
 10419	be angry with you." 
 10420	
 10421	Thus spoke Minerva, and Ulysses obeyed her gladly. Then Minerva assumed
 10422	the form and voice of Mentor, and presently made a covenant of peace
 10423	between the two contending parties. 
 10424	
 10425	THE END
 10426	
 10427	----------------------------------------------------------------------
 10428	
 10429	Copyright statement:
 10430	The Internet Classics Archive by Daniel C. Stevenson, Web Atomics.
 10431	World Wide Web presentation is copyright (C) 1994-2000, Daniel
 10432	C. Stevenson, Web Atomics.
 10433	All rights reserved under international and pan-American copyright
 10434	conventions, including the right of reproduction in whole or in part
 10435	in any form. Direct permission requests to classics@classics.mit.edu.
 10436	Translation of "The Deeds of the Divine Augustus" by Augustus is
 10437	copyright (C) Thomas Bushnell, BSG.
~/CLI_playground$
```

#### Concatenating Files

`cat` is short for "concatenate." This might be a hint that it can be used to combine the contents of multiple files. To do so, provide both files as arguments to `cat`. For example:

```bash
~/CLI_playground$ cat berra_quote.txt einstein_quote.txt
The future ain't what it used to be. - Yogi Berra
Everything should be as simple as possible, but no simpler. - Albert Einstein
~/CLI_playground$
```

## heads and tails

Two complementary commands for inspecting files are `head` and `tail.` `head` shows the first 10 lines of the file. For example:

```bash
~/CLI_playground$ head the_odyssey.txt 
Provided by The Internet Classics Archive.
See bottom for copyright. Available online at
    http://classics.mit.edu//Homer/odyssey.html

The Odyssey
By Homer


Translated by Samuel Butler

~/CLI_playground$ 
```

While `tail` shows the last 10 lines of the file:

```bash
~/CLI_playground$ tail the_odyssey.txt 

Copyright statement:
The Internet Classics Archive by Daniel C. Stevenson, Web Atomics.
World Wide Web presentation is copyright (C) 1994-2000, Daniel
C. Stevenson, Web Atomics.
All rights reserved under international and pan-American copyright
conventions, including the right of reproduction in whole or in part
in any form. Direct permission requests to classics@classics.mit.edu.
Translation of "The Deeds of the Divine Augustus" by Augustus is
copyright (C) Thomas Bushnell, BSG.
~/CLI_playground$
```

These two commands are useful when you only need to view the beginning or end of a file.

## less

`cat` has several drawbacks that make it inconvenient to use for files that span more than a few pages. Most notably, it does not have any useful features for navigating the file’s output; the only way you can navigate the file is by scrolling up and down. an alternative is less.&#x20;

When you open a file with `less`, you can scroll through the document line by line or page by page using keyboard commands. Pressing the `spacebar` scrolls down one screen, and `b` scrolls back one screen. To quit `less`, type '`q'`.

{% hint style="success" %}
The `man` command outputs _with_ `less`, so by getting familair with `less` you’ll get better at navigating _manpages_ as well.
{% endhint %}

A powerful feature of `less` you can search for text within the file by pressing `/` followed by the text you're searching for, and navigate to the next or previous occurrence with `n` or `N`, respectively. For example, suppose we wanted to search for the word "home" in the\_oddysey. The way to do this in `less` is to type `/rose` (read “slash rose”), as shown in [Listing 3.6](https://www.learnenough.com/command-line-tutorial/inspecting\_files#code-rose\_search). The result of pressing return after typing `/rose` in [Listing 3.6](https://www.learnenough.com/command-line-tutorial/inspecting\_files#code-rose\_search) is to highlight the first occurrence of “rose” in the file. You can then press `n` to navigate to the next match, or `N` to navigate to the previous match.

{% hint style="success" %}
The `man` command outputs _with_ `less`, so by getting familair with `less` you’ll get better at navigating _manpages_ as well.
{% endhint %}



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
