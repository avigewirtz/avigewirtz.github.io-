# About This Tutorial

In this book, I describe the Linux programming interface—the system calls, library functions, and other low-level interfaces provided by Linux, a free implementation of the UNIX operating system. These interfaces are used, directly or indirectly, by every program that runs on Linux. They allow applications to perform tasks such as file I/O, creating and deleting files and directories, creating new processes, executing programs, setting timers, communicating between processes and threads on the same computer, and communicating between processes residing on different computers connected via a network. This set of low-level interfaces is sometimes also known as the system programming interface.

Although I focus on Linux, I give careful attention to standards and portability issues, and clearly distinguish the discussion of Linux-specific details from the dis- cussion of features that are common to most UNIX implementations and standardized by POSIX and the Single UNIX Specification. Thus, this book also provides a com- prehensive description of the UNIX/POSIX programming interface and can be used by programmers writing applications targeted at other UNIX systems or intended to be portable across multiple systems.

### Target Audience

This guide is specifically designed for students currently enrolled in _COS217: Introduction to Programming Systems_. As such, it presupposes familiarity with fundamental programming concepts covered in COS126.&#x20;

### Computing Environment

All code examples in this guide have been executed on Princeton's Armlab computer, which runs on the Red Hat Linux distribution. While these examples are anticipated to function on other Unix-like operating systems, such as macOS, minor variations may occur.

### Conventions Used

_Italic_

> Indicates new terms, URLs, and filenames.

`Code blocks`

> Used for URLs, and filenames, as well as within paragraphs to refer to program elements such as variable or function names, data types, environment variables, statements, and keywords.

All-CAPS

> Signifies a placeholder, meaning text that should be substituted with user-provided values. For example, `mkdir DIRECTORY_NAME`  means you should replace `DIRECTORY_NAME` with your own value.
