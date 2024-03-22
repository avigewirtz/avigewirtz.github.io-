# git commit

Committing files in Git means creating a snapshot of the changes you've staged and recording them in the repository's history. This allows you to revert to previous versions if needed.

The general form of a Git commit command is as follows:

```bash
git commit -m "COMMIT_MESSAGE"
```

Where COMMIT\_MESSAGE is replaced with a concise, meaningful description of the changes you made. This message helps you and your collaborators understand the purpose of the commit when reviewing the project's history.

### Common options

* `--amend`: Replaces the last commit with a new one. This can be useful for fixing minor errors or typos or changing the commit message.
* `-a`: Skips git add (i.e., stages and commits all modified files in one command).&#x20;

**Examples**

1. Committing with a detailed message:

```bash
git commit -m "Fixed bug causing the program to segment fault"
```

3. Amending the most recent commit message:

```bash
git commit --amend -m "Bugfix: Corrected typo"
```

4. Stage and commit tracked files in one command:&#x20;

```bash
git commit -a -m "Added function comments"
```

5. Amend a commit and keep the same log message

```bash
git commit --amend --no-edit
```
