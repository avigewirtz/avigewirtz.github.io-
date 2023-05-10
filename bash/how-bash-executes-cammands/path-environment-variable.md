# Path Environment Variable

The PATH environment variable is a variable that specifies the directories the shell should search to find an executable file when there is no / in the program name. By default, the PATH variable usually contains the following directories.

* _/usr/bin_
* _/usr/sbin_
* _/usr/local/bin_
* _/usr/local/sbin_
* _/bin_
* _/sbin_

Thus, when users invoke programs such as `logname`, `hostname`, or `cal`, the shell searches for these programs in the directories listed in `$PATH`. You could also invoke these programs using their absolute or relative pathnames, of course.&#x20;

This shell behavior is often a source of confusion for command-line beginners. Say the executable hello is located in the working directory. Invoking hello will not work, even though it is a valid (relative) pathname–the error “No such file or directory” will be returned.&#x20;

The reason, as we just explained, is that the shell will only search the directories listed in $PATH when a program is invoked without a / in its name. Even if the program is located in the working directory, it still must be invoked using a /. A useful “trick” to invoke hello with a / is to trivially insert a /, as so: ./hello. Because `.` references the working directory, it essentially has no effect on the command other than inserting a /.&#x20;

To see which directories are currently registered under PATH, open a terminal and run `Echo $PATH`.&#x20;
