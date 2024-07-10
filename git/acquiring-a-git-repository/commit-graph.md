# Viewing the Commit History

Now that we have made a few commits, let's take a look at how to view the commit history. The most basic command to view the commit history is `git log`, which displays the history in reverse chronological order. Assuming you've followed along in the previous section, your output should look similar to this:

```bash
$ git log
commit 66ee698d6ffbb16d8e4b3df91f4b8b5f6c9b47d4 (HEAD -> main)
Author: Your Name <your.email@example.com>
Date:   Wed Jul 10 10:32:00 2024 -0400

    appended 'world' to hello.txt

commit b78ab29f564d6fb18c0f7d8f4b8e78b1a7e60fb2
Author: Your Name <your.email@example.com>
Date:   Wed Jul 10 09:58:00 2024 -0400

    initial commit with hello.txt, hi.txt, and bye/bye.txt
```

We see two commit entries, each with four pieces of information:

1. **Commit Hash:** A unique identifier for each commit, for example, `66ee698d6ffbb16d8e4b3df91f4b8b5f6c9b47d4`. This hash can be used to refer to a specific commit in various Git commands.
2. **Author:** The name and email of the person who made the commit, such as `Your Name <your.email@example.com>`.
3. **Date:** The date and time when the commit was made, e.g., `Wed Jul 10 10:32:00 2024 -0400`.
4. **Commit Message:** A brief description of the changes introduced in the commit, for example, `appended 'world' to hello.txt`.

At this point we only have two commits in your repo history which makes it easier to read the output easily. For repositories with many commit histories, this standard view may not help you to traverse a long list of detailed commit information with ease; In such situations you can provide the --oneline switch to list a summarized commit ID number along with the commit message.

