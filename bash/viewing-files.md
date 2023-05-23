# Viewing Files

You can view the contents of files using the `cat` (concatenate) command, which (by default) prints the output on the screen. It's syntax is as follows: <mark style="color:red;">**`cat`**</mark><mark style="color:green;">**`OPTION(S)`**</mark><mark style="color:blue;">**`FILE(S)`**</mark>.

<details>

<summary>Common options</summary>

* **`-n`**: Numbers all output lines.

<!---->

* **`-s`**: Squeezes consecutive blank lines into a single blank line.

</details>

## Exercises

1. Print _berra\_qoute.txt_ on the screen:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 4.48.26 PM.png" alt=""><figcaption></figcaption></figure>

2. Concatenate _berra\_quote.txt_ and _einstein\_quote.txt_ and display the result on screen with line numbers:&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 4.48.33 PM.png" alt=""><figcaption></figcaption></figure>

### Limitations of cat

`cat` has two main drawbacks. First, It prints the entire on stdout. This can cause issues when the file is extremely large. For example, say you print _encyclopaedia.txt_ with cat:&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 4.49.17 PM.png" alt=""><figcaption></figcaption></figure>

Because the file is extremely large (almost 100,000 lines!), printing all the output takes quite some time, and your terminal will be unusable until it is complete. Once the printing is finally complete, the final page of the file will be displayed: &#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 4.49.28 PM.png" alt=""><figcaption></figcaption></figure>

The second drawback of `cat` is it does not have any useful features for navigating the file’s output; the only way you can navigate the file is by scrolling up and down.&#x20;

To address these shortcomings with `cat`, other tools were developed. A popular alternative is the  `less` pager, which addresses the limitations of `cat` by (1) printing output one screenful (page) at a time; and (2) adding many useful file navigation features. It also contains many additional useful features, such as searching and highlighting. The syntax for `less` is as follows:<mark style="color:red;">**`less`**</mark><mark style="color:green;">**`OPTION(S)`**</mark><mark style="color:blue;">**`FILE(S)`**</mark>.

<details>

<summary>Common options</summary>

* **`-m`**: Displays the percentage of the cursor's position in the file.

<!---->

* **`-n`**: Numbers output lines.

<!---->

* **`-s`**: Squeezes consecutive blank lines into a single line.

</details>

### Exercises

1. Print _encyclopaedia.txt_ on stdout one page at a time. Suppress repeated blank lines, add line numbers, and display the percentage of the file displayed so far: &#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 4.49.44 PM.png" alt=""><figcaption></figcaption></figure>

The following page will be displayed on stdout:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-26 at 4.49.52 PM.png" alt="" width="563"><figcaption></figcaption></figure>

You can navigate the `less` output using the following keystrokes:&#x20;

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
