# What commands represent

<figure><img src="../../.gitbook/assets/Group 37.png" alt=""><figcaption></figcaption></figure>

One of the most basic functions of Bash is to launch other programs for you. The program it launches might be a program like _date_, which comes with all Unix systems, or it might be a simple user-written program like hello, which writes "Hello, World!" on stdout. From Bash's perspective, there's no real difference between programs like date and hello, except that by default, date can be launched by just typing it's name, whereas to launch hello you must type it's pathname

```bash
$ /bin/date 
Mon Mar 25 21:10:49 EDT 2023
$ ../../bin/date
Mon Mar 25 21:11:47 EDT 2023
$ 
```

```
$ date
Mon Mar 25 21:15:25 EDT 2024
$ 
```
