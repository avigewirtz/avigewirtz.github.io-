# Table of contents

## Preface

* [About This Tutorial](README.md)
* [Organization of this tutorial](preface/organization-of-this-tutorial.md)

## Armlab

* [Armlab](armlab/armlab/README.md)
  * [Activating Your Armlab Account](armlab/armlab/activating-your-armlab-account.md)
  * [Logging Into and Out of Armlab](armlab/armlab/logging-into-armlab.md)
  * [Secure Shell (SSH) Protocol](armlab/armlab/ssh-protocol.md)
  * [Configuring Your Armlab Environment](armlab/armlab/configuring-your-armlab-environment.md)

## The Linux command line

* [Introduction](the-linux-command-line/introduction.md)
* [First Command-Line Session](the-linux-command-line/warm-up-commands.md)
* [Understanding the CLI](the-linux-command-line/understanding-the-cli.md)
* [A Tour of Linux](the-linux-command-line/a-tour-of-linux/README.md)
  * [Users and Groups](the-linux-command-line/a-tour-of-linux/users-and-groups.md)
  * [The Filesystem](the-linux-command-line/a-tour-of-linux/filesystem.md)
* [Navigating the Filesystem](the-linux-command-line/navigating-the-filesystem/README.md)
* [Aliases](the-linux-command-line/useful-command-line-features.md)
* [Getting Documentation for Commands](the-linux-command-line/getting-help.md)
* [Redirection and Piping](the-linux-command-line/redirection-and-piping.md)
* [Basic File and Directory Operations](the-linux-command-line/basic-file-and-directory-operations/README.md)
  * [Creating Files and Directories](the-linux-command-line/basic-file-and-directory-operations/creating-files-and-directories.md)
  * [Deleting Files and Directories](the-linux-command-line/basic-file-and-directory-operations/deleting-files-and-directories.md)
  * [Viewing Files](the-linux-command-line/basic-file-and-directory-operations/viewing-files.md)
  * [Copying, Moving, and Renaming Files/Directories](the-linux-command-line/basic-file-and-directory-operations/copying-files-and-directories.md)
* [Viewing User and Group Information](the-linux-command-line/viewing-user-and-group-information.md)
* [File and Directory Access Permissions](the-linux-command-line/file-and-directory-access-permissions.md)
* [More advanced topics](the-linux-command-line/more-advanced-topics/README.md)
  * [Processes](the-linux-command-line/more-advanced-topics/processes.md)
  * [Bash Execution Environment](the-linux-command-line/more-advanced-topics/bash-execution-environment.md)
  * [Revisiting Redirection and Piping](the-linux-command-line/more-advanced-topics/revisiting-redirection-and-piping.md)
  * [How Bash Executes Cammands](the-linux-command-line/more-advanced-topics/how-bash-executes-cammands.md)
* [Linux CLI Cheat Sheet](the-linux-command-line/bash-cheat-sheet.md)
* [Further Reading](the-linux-command-line/further-reading.md)

## Git

* [Introduction](git/background/README.md)
  * [Installing Git](git/background/installing-git.md)
  * [Getting Documentation for Git Commands](git/background/getting-help.md)
  * [Git configuration files](git/background/git-configuration-files.md)
  * [Git in a nutshell](git/git-in-a-nutshell.md)
* [Local Workflow Fundamentals](git/acquiring-a-git-repository/README.md)
  * [Components of a Git Project](git/acquiring-a-git-repository/components-of-a-git-project.md)
  * [Recording Changes to the Repository](git/acquiring-a-git-repository/recording-changes-to-the-repository.md)
  * [Viewing the Commit History](git/acquiring-a-git-repository/commit-graph.md)
  * [Understanding the Commit ID](git/acquiring-a-git-repository/how-git-identifies-commits.md)
  * [Going Back in History](git/acquiring-a-git-repository/going-back-in-history.md)
* [Branching](git/branching/README.md)
  * [Merging](git/branching/merging/README.md)
    * [How 3-way merges work](git/branching/merging/how-3-way-merges-work.md)
    * [Merge examples](git/branching/merging/merge-examples.md)
    * [Resolving merge conflicts](git/branching/merging/resolving-merge-conflicts.md)
* [Working with remotes](git/working-with-remotes-1/README.md)
  * [Single-developer remote workflow](git/working-with-remotes-1/single-developer-remote-workflow.md)
  * [Multi-developer remote workflow](git/working-with-remotes-1/working-with-collaborator.md)
  * [cloning](git/working-with-remotes/cloning.md)
  * [Pushing and Fetching/Pulling](git/working-with-remotes-1/pushing-and-pulling.md)
* [Undoing things](git/undoing-things.md)
  * [Rebasing](git/acquiring-a-git-repository/rebasing.md)
* [GitHub](git/github/README.md)
  * [Creating a GitHub Account](git/github/creating-github-account.md)
  * [Creating a Git Repository on GitHub](git/github/creating-a-git-repository-on-github.md)
  * [Generating a Personal Access Token](git/github/generating-a-personal-access-token.md)
  * [Adding a Collaborator To Your GitHub Repository](git/github/adding-a-collaborator-to-your-github-repository.md)
* [Miscellaneous](git/important-git-commands/README.md)
  * [Diffs](git/important-git-commands/diffs.md)
  * [Tags](git/important-git-commands/tags.md)
  * [Ignoring Files](git/important-git-commands/ignoring-files.md)
* [COS217 Specific](git/acquiring-cos217-assignment-repositories/README.md)
  * [COS217 Development Workflow](git/acquiring-cos217-assignment-repositories/cos217-development-workflow.md)
* [Git Cheatsheet](git/git-cheat-sheet.md)
* [Further Reading](git/further-reading.md)

## GCC Build Process

* [Introduction](gnu-compiler-collection-gcc/introduction.md)
* [The Big Picture](gcc-build-process/the-four-stage-build-process.md)
* [Example: charcount.c](gcc-build-process/example-single-file-program.md)
* [Building Multi-file Programs](gcc-build-process/page-1-1.md)
* [Identifying Cause of Build Errors](gcc/identifying-build-errors.md)
* [GCC Cheatsheet](gnu-compiler-collection-gcc/gcc-cheatsheet.md)
* [Further Reading](copy-of-gnu-compiler-collection-gcc/further-reading.md)

## Make

* [Introduction](make/background.md)
* [How Incremental Builds Work in C](make/incremental-builds.md)
* [Automating Incremental Builds With make](make/makefiles.md)
* [Writing a Simple Makefile](make/writing-a-simple-makefile.md)
* [Running make](make/running-make.md)
* [How make Processes a Makefile](make/how-make-processes-a-makefile.md)
* [Phony Targets](make/makefile-version-2-phony-targets.md)
* [Macros](make/makefile-version-3-macros.md)
* [Advanced Features](make/implicit-rules.md)
* [Further Reading](make/further-reading.md)

## Gprof

* [Background](gprof/background.md)
* [How Gprof Works](gprof/how-gprof-works.md)
* [Using Gprof](gprof/using-gprof.md)
* [Interpreting Gprof Output](gprof/interpreting-gprof-output.md)
  * [Flat Profile](gprof/interpreting-gprof-output/flat-profile.md)
  * [Call Graph](gprof/interpreting-gprof-output/call-graph.md)

## Appendices

* [Compiler and Assembler](gcc-build-process/compiler-and-assembler.md)
