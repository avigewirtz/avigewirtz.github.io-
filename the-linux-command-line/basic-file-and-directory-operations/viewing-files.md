# Viewing Files

There are numerous commands you can use to view the contents of a file. In this section we'll cover four of them: `cat`, `head`, `tails`, and `less`.&#x20;

### cat

A quick and easy way to view a file is with the `cat` command, which displays the file's contents on stdout. Type `cat` followed by the name of the file you want to view. For example, to view `berra_quote.txt`:

```bash
~/CLI_playground$ cat berra_quote.txt
The future ain't what it used to be. - Yogi Berra
~/CLI_playground$
```

#### **Displaying Line Numbers**

If you want the file's output to have line numbers, invoke `cat` with the `-n` option. For example:

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

#### **Combining Multiple Files**

`cat` is short for "concatenate," which might be a hint that it can be used to combine the contents of multiple files. Type `cat` followed by the name of each file you want cat to combine. For example, to combine `berra_quote.txt` and `einstein_quote.txt` :

```bash
~/CLI_playground$ cat berra_quote.txt einstein_quote.txt
The future ain't what it used to be. - Yogi Berra
Everything should be as simple as possible, but no simpler. - Albert Einstein
~/CLI_playground$
```

If you want to save the combined content in a new file, you can redirect the output using the `>` operator:&#x20;

```bash
cat berra_quote.txt einstein_quote.txt > combined_quotes.txt.txt
```

### heads and tails

Two complementary commands for inspecting files are `head` and `tail.` `head` shows the first 10 lines of the file:

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

### less

`cat` has several drawbacks that make it inconvenient to use with files that span more than a few pages. Most notably, it does not have any useful features for navigating the file’s output.&#x20;

A useful alternative is `less`, which enables you to scroll through the file line by line or page by page using keyboard commands. Pressing `spacebar` scrolls forward one screen, and `b` scrolls back one screen. To quit `less`, type `q`.

A powerful feature of `less` is the ability to search for text within the file. Press `/` followed by the text you're searching for. For example, to search for the word "home" in `the_odyssey.txt`, type `/home` in `less`. After pressing return, the first occurrence of "home" in the file will be highlighted. Use `n` to navigate to the next occurrence, or `N` to navigate to the previous occurrence. Table 2 summarizes commonly used `less` commands.

| Command                 | Effect                                      |
| ----------------------- | ------------------------------------------- |
| `q`                     | Quit                                        |
| `h`                     | Display a list of available `less` commands |
| `UP-ARROW / DOWN-ARROW` | Navigate up and down the file               |
| `SPACEBAR`              | Go forward one page                         |
| `b`                     | Go backward one page                        |
| `G`                     | Go to end of file                           |
| `g`                     | Go to beginning of file                     |
| `/pattern`              | Search file for text matching “pattern”     |

{% hint style="success" %}
The `man` command displays its output with `less`, so by getting familiar with `less`, you’ll get better at navigating manpages as well.
{% endhint %}

### Exercises

1. **Which command is most suitable for viewing and navigating a long text file?**
   * A) `cat`
   * B) `less`
   * C) `head`
   * D) `echo`
2. **Which `cat` command option will number all output lines when viewing files?**
   * A) `-b`
   * B) `-n`
   * C) `-s`
   * D) `-e`
3. **What does pressing `G` do when you are navigating a file using `less`?**
   * A) Goes to the beginning of the file.
   * B) Goes to the end of the file.
   * C) Finds the next occurrence of a search.
   * D) Scrolls down one page.
4. **If you want to view the contents of `file1.txt` followed by `file2.txt` in a single command using `cat`, and then redirect the output to `combined.txt`, which command would you use?**
   * A) `cat file1.txt; cat file2.txt > combined.txt`
   * B) `cat file1.txt > combined.txt; cat file2.txt >> combined.txt`
   * C) `cat file1.txt file2.txt > combined.txt`
   * D) `cat file1.txt + file2.txt > combined.txt`
5. **What happens when you use the `cat` command without specifying any files?**
   * A) It deletes the contents of the default file.
   * B) It creates a new file.
   * C) It reads from standard input.
   * D) It shows the help information.
6. **Which of the following keys can you press while using `less` to search for a text string?**
   * A) `f`
   * B) `n`
   * C) `g`
   * D) `/`

<details>

<summary>Answers to exercises</summary>

1. B
2. B
3. B
4. C
5. C
6. D

</details>
