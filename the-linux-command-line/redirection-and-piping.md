# Redirecting Input and Output

When a program is started up, it by default has three data streams attached to it: one for reading input, one for writing normal output, and one for writing diagnostic or error messages. These streams are known as standard input (stdin), standard output (stdout), and standard error (stderr) respectively.&#x20;

Consider the following C program, for example, that...

{% code title="number.c" lineNumbers="true" %}
```c
#include <stdio.h>

int main() {
    int number;

    printf("Enter a number:\n");
    if (scanf("%d", &number) != 1) {
        fprintf(stderr, "Error: Invalid input.\n");
        return 1; 
    }

    printf("You entered: %d\n", number);

    return 0;
}
```
{% endcode %}

scanf reads from stdin, which by default is the text entered into the terminal. printf prints to stdout, which by default is also the terminal. When we run the program, it reads a number from stdin. By default, stdin is entered by the user in the terminal.&#x20;

```
~> ./number
Enter a number:
2
You entered: 2
~> 
```

When it writes the number, it writed it to stdout. By default, stdout is also connected to the terminal.&#x20;



The shell offers a mechanism to redirect the source of stdin and stdout.&#x20;

You can redirect where the input

When a program is started up, it by default has three data streams attached to it: one for reading input, one for writing normal output, and one for writing diagnostic or error messages. These streams are known as standard input (stdin), standard output (stdout), and standard error (stderr) respectively.&#x20;

When we write C programs, we typically interact with these streams by using library functions such as printf and scanf. printf prints to stdout, which is connected to the terminal screen, and scanf reads from stdin, which is connected to the terminal keyboard.&#x20;

A useful feature of the shell is that it can change the default behavior of these three streams. For example, it can start a program such as hello.c, but it can decide beforehand that instead of hello world being printed on the terminal screen, it should be sent to a file, such as hello.txt.&#x20;





```c
#include <stdio.h>

int main() {
    int number;

    printf("Enter a number:\n");
    scanf("%d", &number);
    printf("You entered: %d\n", number);

    return 0;
}
```



## Redirection

Redirection refers to the process of changing where the input of a command originates from or where the output of a command is directed to. There are three main types of redirection:

1. Standard input redirection (`<`): This replaces the default stdin source (keyboard) with a file. For example, you can use the 'cat' command to read the content of a file and display it on the terminal screen:

```bash
cat < input.txt # Reads the content of 'input.txt' and displays it on the terminal.
```

2. Standard output redirection (`>` and `>>`): This redirects stdout to a file instead of the screen. The `>` operator overwrites the file, while `>>` appends to it. For example, you can save the output of the `cat` command to a file:

```bash
cat input.txt > output.txt  # Overwrites output.txt with the content of input.txt
cat another_input.txt >> output.txt  # Appends the content of another_input.txt to output.txt
```

3. Standard error redirection (`2>` and `2>>`): This redirects stderr to a file instead of the screen. Like output redirection, `2>` overwrites the file, and `2>>` appends to it. For example, you can redirect error messages from the 'less' command:

```bash
less nonexistent_file 2> errors.txt  # Overwrites errors.txt with error messages
less another_nonexistent_file 2>> errors.txt  # Appends error messages to errors.txt
```

## Piping

_Piping_ (`|`) is the process of connecting the output of one command to the input of another command, allowing you to chain multiple commands together. For example, you can use the `cat` command to send the content of a file to the `sort` command:

```bash
cat file.txt | sort
```

The pipe (`|`) takes the output of `cat` and feeds it as input to `sort`, which sorts the file's contents and displays the output on the terminal screen.

### Exercises

1. Redirect the standard output of `ls` to a file:&#x20;

```bash
ls > file.txt
```

2. Append the standard output of `ls` to a file:

```bash
ls >> file.txt
```

3. Sort the contents of the working directory and print the result on the screen:&#x20;

```bash
ls | sort
```

4. Count the total number of lines in `einstein_quote.txt`:

```bash
cat einstein_quote.txt | wc -w
```

5. Sort the contents of the working directory and save the output in a file:

```bash
ls | sort > sorted_file_list.txt
```

6. Sort `einstein_quote.txt` alphabetically, writing the output to `sorted_einstein_quote.txt`:

```bash
sort einstein_quote.txt > sorted_einstein_quote.txt
```

7. Count the total number of lines in `einstein_quote.txt` and `the_odyssey.txt`:

```bash
cat einstein_quote.txt the_odyssey.txt | wc -l
```

{% hint style="info" %}
**Reference sheet**

* `COMMAND > FILE`: Redirect the output of a command to a file (overwrite).
* `COMMAND >> FILE`: Redirect the output of a command to a file (append).
* `COMMAND < FILE`: Redirect the contents of a file to a command as input.
* `COMMAND 2> FILE`: Redirect the error output of a command to a file.
* `COMMAND1 | COMMAND2`: Pipe the output of one command as input to another command\

{% endhint %}
