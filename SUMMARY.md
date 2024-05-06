# Table of contents

## Preface

* [About This Tutorial](README.md)
* [Organization of this tutorial](preface/organization-of-this-tutorial.md)
* [Conventions used](preface/conventions-used.md)
* [Acknowledgments](preface/acknowledgments.md)

## Armlab

* [Armlab](armlab/armlab/README.md)
  * [Activating Your Armlab Account](armlab/armlab/activating-your-armlab-account.md)
  * [Logging Into and Out of Armlab](armlab/armlab/logging-into-armlab.md)
  * [Secure Shell (SSH) Protocol](armlab/armlab/ssh-protocol.md)
  * [Configuring Your Armlab Environment](armlab/armlab/configuring-your-armlab-environment.md)

## The Linux command line

* [Introduction](the-linux-command-line/introduction/README.md)
  * [Linux Kernel](the-linux-command-line/introduction/linux-kernel.md)
  * [The Bash shell](the-linux-command-line/introduction/the-bash-shell.md)
  * [Linux Filesystem](the-linux-command-line/introduction/filesystem/README.md)
* [Getting Started With Bash](the-linux-command-line/warm-up-commands.md)
* [Bash Shortcuts](the-linux-command-line/useful-command-line-features/README.md)
  * [Command history](the-linux-command-line/useful-command-line-features/command-history.md)
  * [Aliases](the-linux-command-line/useful-command-line-features/aliases.md)
  * [Wildcards](the-linux-command-line/useful-command-line-features/wildcards.md)
* [Navigating the Filesystem](the-linux-command-line/navigating-the-filesystem/README.md)
* [Getting Documentation For Commands](the-linux-command-line/getting-help.md)
* [Basic File and Directory Operations](the-linux-command-line/basic-file-and-directory-operations/README.md)
  * [Creating Files and Directories](the-linux-command-line/basic-file-and-directory-operations/creating-files-and-directories.md)
  * [Deleting Files and Directories](the-linux-command-line/basic-file-and-directory-operations/deleting-files-and-directories.md)
  * [Viewing Files](the-linux-command-line/basic-file-and-directory-operations/viewing-files.md)
  * [Copying, Moving, and Renaming Files/Directories](the-linux-command-line/basic-file-and-directory-operations/copying-files-and-directories.md)
* [Redirection and Piping](the-linux-command-line/redirection-and-piping.md)
* [Users Accounts](the-linux-command-line/users-and-groups.md)
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
  * [Goals of this tutorial](git/background/goals-of-this-tutorial.md)
  * [Installing Git](git/background/installing-git.md)
  * [First time Git setup](git/background/git-installation.md)
  * [Getting Documentation for Git Commands](git/background/getting-help.md)
  * [Git configuration files](git/background/git-configuration-files.md)
* [Git in a nutshell](git/git-in-a-nutshell.md)
* [Beginner Local Workflow](git/acquiring-a-git-repository/README.md)
  * [Setting up a git project](git/acquiring-a-git-repository/setting-up-a-git-project.md)
  * [Understanding the index](git/acquiring-a-git-repository/understanding-the-index.md)
  * [Recording changes to repository](git/acquiring-a-git-repository/recording-changes-to-repository.md)
  * [Commits](git/acquiring-a-git-repository/commit-graph.md)
* [Intermediate local workflow: branching and merging](git/intermediate-local-workflow-branching-and-merging/README.md)
  * [Branching](git/acquiring-a-git-repository/branching.md)
  * [Merging](git/acquiring-a-git-repository/merging/README.md)
    * [How 3-way merges work](git/acquiring-a-git-repository/merging/how-3-way-merges-work.md)
    * [Merge examples](git/acquiring-a-git-repository/merging/merge-examples.md)
    * [Resolving merge conflicts](git/acquiring-a-git-repository/merging/resolving-merge-conflicts.md)
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
* [The Big Picture](copy-of-gnu-compiler-collection-gcc/the-four-stage-build-process/README.md)
* [Deeper dive](gcc-build-process/page-1/README.md)
  * [Preprocessing stage](gcc-build-process/page-1/preprocessing-stage.md)
  * [Compilation stage](gcc-build-process/page-1/compilation-stage.md)
  * [Assembly stage](gcc-build-process/page-1/assembly-stage.md)
  * [Linking stage](gcc-build-process/page-1/linking-stage.md)
* [Key takeaways](gcc-build-process/key-takeaways.md)
* [Identifying Build Errors](gcc/identifying-build-errors.md)
* [GCC Cheatsheet](gnu-compiler-collection-gcc/gcc-cheatsheet.md)
* [Further Reading](copy-of-gnu-compiler-collection-gcc/further-reading.md)

## Make

* [Introduction](make/background.md)
* [Makefiles](make/makefiles/README.md)
  * [Dependency graphs](make/makefiles/dependency-graphs.md)
  * [Writing a Makefile](make/makefiles/makefile-version-1-basic.md)
  * [How make processes a Makefile](make/makefiles/how-make-processes-a-makefile.md)
  * [Phony targets](make/makefiles/makefile-version-2-phony-targets.md)
  * [Macros](make/makefiles/makefile-version-3-macros.md)
* [Further Reading](make/further-reading.md)

## Emacs

* [Introduction](emacs/background.md)
* [Emacs Interface](emacs/fundamentals/README.md)
* [Getting Started](emacs/basic-commands/README.md)
  * [Launching and Exiting Emacs](emacs/basic-commands/launching-and-existing-emacs.md)
  * [Moving the cursor](emacs/basic-commands/moving-the-cursor.md)
  * [Selecting a Region](emacs/basic-commands/selecting-a-region.md)
  * [Basic Editing Commands](emacs/basic-commands/basic-editing-commands.md)
* [More Advanced Commands](emacs/more-advanced-commands/README.md)
  * [Managing Windows and Buffers](emacs/more-advanced-commands/managing-windows-and-buffers.md)
  * [Search and Replace](emacs/more-advanced-commands/search-and-replace.md)
  * [Building](emacs/more-advanced-commands/building.md)
* [Emacs Cheat Sheet](emacs/emacs-cheat-sheet.md)
* [Further Reading](emacs/further-reading.md)

## Gprof

* [Background](gprof/background.md)
* [How Gprof Works](gprof/how-gprof-works.md)
* [Using Gprof](gprof/using-gprof.md)
* [Interpreting Gprof Output](gprof/interpreting-gprof-output.md)
  * [Flat Profile](gprof/interpreting-gprof-output/flat-profile.md)
  * [Call Graph](gprof/interpreting-gprof-output/call-graph.md)

## Appendices

* [Assembly](appendices/assembly.md)
* [Machine Code](appendices/machine-code.md)

## Group 1

* [Glossary](appendices/glossary.md)
