# Introduction

* what is emacs
* uses keystrokes rather than mouse&#x20;

## Emacs Modes

Emacs operates in various _modes_. Modes provide language-specific or file-format-specific features, such as syntax highlighting, indentation, and code completion, making editing and navigating files easier.&#x20;

Within the scope of COS217, you will primarily work with four modes: C mode, Assembler mode, Text mode, and Fundamental mode. Emacs automatically selects the appropriate mode based on the filename extension:

* .c: C mode
* .s: Assembler mode
* .txt: Text mode
* No extension: Fundamental mode

## Keystrokes&#x20;

Before exploring Emacs commands, it's important to familiarize yourself with the standard notation used for key sequences. Here are a few examples of key sequence notation used in this tutorial:

* **C-x**: Hold the Control key and press the "x" key.
* **C-x C-c**: Hold the Control key and press the "x" key, then release both keys and hold the Control key again while pressing the "c" key.
* **C-x 1**: Hold the Control key and press the "x" key, then release both keys and press the "1" key.
* **C-x l 5**: Hold the Control key and press the "x" key, then release both keys and press the "l" key, then release "I" key and press the "5" key.
* **C-x C-w file**: Hold the Control key and press the "x" key, then release both keys and hold the Control key again while pressing the "w" key. After that, release both keys and type the desired file name (replacing "file" with the actual file name) and press "Enter" or "Return" to complete the command.&#x20;



## Single File example

hello.c.&#x20;

```
emacs hello.c
```

You should see the following:

<figure><img src="../.gitbook/assets/Screenshot 2024-03-14 at 9.18.48 PM.png" alt=""><figcaption></figcaption></figure>

* **Buffers**: Buffers are the in-memory representation of files, or temporary workspaces for text. Every file you open in Emacs is loaded into a buffer. You can have multiple buffers open, even if they are not visible in any window. Buffers also store changes made to text before you save them to disk.
* **Window**: A window in Emacs displays a buffer. You can have multiple windows open, each showing a different buffer.
* **Frame**: A frame is the entire graphical window that holds one or more Emacs windows.
* **Point**: The point is the current position of the text cursor in a buffer.
* **Mode Line**: Located at the bottom of each window, the mode line displays essential information about the buffer shown in that window. It includes the buffer's name, the current [mode(s)](broken-reference), the position of the cursor, and other useful details, such as whether the buffer has unsaved changes.
