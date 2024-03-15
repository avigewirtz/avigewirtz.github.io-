# Launching and Exiting Emacs

### Launching Emacs

Run `emacs file_name` on the command line. Emacs will launch and open the specified file in a new buffer. If the specified file doesn't exist, Emacs will create a new buffer with the specified name.

### Exiting Emacs

You can exit Emacs by invoking `C-x C-c`. If you have unsaved changes, Emacs will prompt you to save the changes before exiting.

### Moving the Cursor

* Move one character forward: `C-f`&#x20;
* Move one character backward: `C-b`&#x20;
* Move one line up: `C-p`&#x20;
* Move one line down: `C-n`&#x20;
* Move to the beginning of the line: `C-a`&#x20;
* Move to the end of the line: `C-e`&#x20;
* Move forward one word: `M-f` (Alt + f or ESC + f)
* Move backward one word: `M-b` (Alt + b or ESC + b)
* Move to the beginning of the buffer: `M-<` (Alt + Shift + < or ESC + Shift + <)
* Move to the end of the buffer: `M->` (Alt + Shift + > or ESC + Shift + >)

Note that `C` stands for "Control" and `M` stands for "Meta" (which is typically the Alt key on most keyboards).

These are just a few of the cursor movement commands in Emacs. You can find a more comprehensive list by pressing `C-h r` and navigating to the relevant sections.

### Selecting a Region

