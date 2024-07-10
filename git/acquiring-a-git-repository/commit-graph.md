# Viewing the Commit History

Now that we have made a few commits, let's take a look at how to view the commit history. The most basic command to view the commit history is `git log`, which displays the commit history in reverse chronological order, meaning the most recent commit appears first. Assuming you have followed along with the previous sections, your output should look similar to this:

```git
$ git log
commit eb145a198ea3c47cd0e8b3923f5bb960b672602e (HEAD -> main)
Author: Avi Gewirtz <sgewirtz@princeton.edu>
Date:   Sat Apr 6 21:57:29 2024 -0400

    appended 'world' to hello.txt

commit f8b9623a5c34f22f6e8e6bf9b5a438d3e2a8c1b2
Author: Avi Gewirtz <sgewirtz@princeton.edu>
Date:   Sat Apr 6 20:45:12 2024 -0400

    added hi.txt

commit c0d3628d5a4eab36c3bba5d3f1d0459b6b5b3c1c
Author: Avi Gewirtz <sgewirtz@princeton.edu>
Date:   Sat Apr 6 20:30:45 2024 -0400

    created bye directory with bye.txt

commit b6a24e7a7c84d1e6b3a36f1b0c3d5e9d2a5c3b2d
Author: Avi Gewirtz <sgewirtz@princeton.edu>
Date:   Sat Apr 6 20:15:11 2024 -0400

    initial commit with hello.txt and hi.txt

commit a7d3627a6e34f22f3e8e6bf9b5a438d3e2a8b1a1
Author: Avi Gewirtz <sgewirtz@princeton.edu>
Date:   Sat Apr 6 20:00:45 2024 -0400

    added project setup

commit 9d2e8f6a3c24d1e3b6a35f1c0d3d5e9d1a5c3b2c
Author: Avi Gewirtz <sgewirtz@princeton.edu>
Date:   Sat Apr 6 19:45:23 2024 -0400

    created initial structure

```

We see six commit entries, each with four pieces of information. Let's break it down using the most recent commit as an example:

*   commit eb145a198ea3c47cd0e8b3923f5bb960b672602e (HEAD -> main)

    This seemingly gibberish string is a 40 digit hex number that git uses to identify the commit. We'll elaborate on this in Commit ID. Note that your commit ID will be different than this, even if the content of your commit snapshot is identical.&#x20;


*   Author: Avi Gewirtz \<sgewirtz@princeton.edu>.&#x20;

    Name and email of the commit author. Git gets this information from the .git/config file.&#x20;


*   Date:   Sat Apr 6 21:57:29 2024 -0400.&#x20;

    This is the timestamp of when the commit was made.
*   appended 'world' to hello.&#x20;

    This is the commit message, describing the changes made in this commit..&#x20;



At this point, we only have six commits in our repository history, making it easy to read the output. For repositories with extensive commit histories, this standard view may not be ideal. Instead, you can use the `--oneline` option, which shortens each commit entry to one line, showing only the first seven digits of the commit ID and the commit message:

```
$ git log --oneline
eb145a1 (HEAD -> main) appended 'world' to hello.txt
f8b9623 added hi.txt
c0d3628 created bye directory with bye.txt
b6a24e7 initial commit with hello.txt and hi.txt
a7d3627 added project setup
9d2e8f6 created initial structure
```
