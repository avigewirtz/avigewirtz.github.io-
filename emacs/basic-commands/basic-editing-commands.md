# Basic Editing Commands

## Inserting text

* Just start typing

## Deleting text

* Delete the character before the cursor: `C-h` or `DEL` (Backspace)
* Delete the character at the cursor: `C-d`&#x20;
* Delete the word before the cursor: `M-DEL` (Alt + Backspace or ESC + Backspace)
* Delete the word after the cursor: `M-d` (Alt + d or ESC + d)
* Delete from the cursor to the end of the line: `C-k` (
* Delete from the cursor to the beginning of the line: `C-u` or `C-x DEL`&#x20;
* Delete from the cursor to the end of the sentence: `M-k` (Alt + k or ESC + k)

## Undo/redo

* Undo the last change: `C-/`, `C-x u`, or `C-_`&#x20;
* Redo the last change: `C-x C-/`, `C-x C-_`, or `C-g C-/`&#x20;

## Copy/paste

* Cut (kill) selected region: `C-w`&#x20;
* Copy selected region: `M-w` (Alt + w or ESC + w)
* Paste (yank) the last killed text: `C-y`&#x20;
* Paste (yank) the text before the last killed text: `M-y` (Alt + y or ESC + y) - Use this command after `C-y`
* Cut (kill) selected region: `C-w` (Contr

### Saving and Opening Files

* Save a file: C-x C-s
* Save a file with a new name: C-x C-w
* Open a file: C-x C-f
