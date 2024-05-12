# Page

#### 3.104 Command

A directive to the shell to perform a particular task.







Commands come in all shapes an sizes. Essentially anything that you type in the terminal that is valid Bash syntax is a command. One of the most basic functions of the shell is to run other programs for you.&#x20;



## The shell: A program that run other programs

The shell is a command language interpreter.

To some extent, not much&#x20;



## What's a command?

Commands come in all shapes an sizes. Essentially anything that you type in the terminal that is valid Bash syntax is a command. One of the most basic functions of the shell is to run other programs for you.&#x20;





Most commonly, a command consists of a program name followed by zero or more arguments:

```bash
program_name arg1 arg2 ... argN
```

Consider the `cal` command, for example. `cal` is a program, located somewhere in the filesystem. When we type `cal` and press RETURN, it displays the calendar of the current month on the terminal window:

```bash
~/CLI_playground$ cal
   November 2023      
Su Mo Tu We Th Fr Sa  
       1  2  3  4  5  
 6  7  8  9 10 11 12  
13 14 15 16 17 18 19  
20 21 22 23 24 25 26  
27 28 29 30           
                      
~/CLI_playground$
```

This is the default behavior of `cal`. We can also invoke cal with arguments, such as a specific. For example, if we invoke `cal may`, it displays the calendar for the entire year of 2023:

```bash
~/CLI_playground> cal may 2023
      May 2023        
Su Mo Tu We Th Fr Sa  
    1  2  3  4  5  6  
 7  8  9 10 11 12 13  
14 15 16 17 18 19 20  
21 22 23 24 25 26 27  
28 29 30 31           
                      
~/CLI_playground> 
```

#### Syntax of arguments

The specific syntax
