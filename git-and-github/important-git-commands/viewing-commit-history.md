# Viewing Commit History

You can view the commit history of a Git repository using the `git log`. This command displays a log of all the commits in the repository, showing each commit's unique identifier (hashes), author information, date, and commit message.&#x20;

The `git log` command has many options and filters that allow you to customize the output to fit your needs. Here are some common variations of the command:

1.  Compact view with one line per commit:

    ```bash
    git log --oneline
    ```
2.  Show commit history with a graph representation of branches and merges:

    ```bash
    git log --graph
    ```
3.  Limit the number of commits displayed:

    ```bash
    git log -n NUMBER_OF_COMMITS
    ```
4.  Show commit history within a specific date range:

    ```bash
    git log --since=START_DATE --until=END_DATE
    ```

    ates can be in various formats, such as "2 weeks ago", "2022-03-01", or "yesterday".
5.  Filter commit history by author:

    ```bash
    git log --author=AUTHOR_NAME
    ```
6.  Show commit history for a specific file or directory:

    ```bash
    git log -- FILE_OR_DIRECTORY_PATH
    ```

These are just a few examples of how to use the `git log` command. To learn more about the available options, you can use the Git help option: `git log --help`.
