# Table of contents

## Preface

* [About This Tutorial](README.md)
* [Organization of this tutorial](preface/organization-of-this-tutorial.md)
* [Conventions used](preface/conventions-used.md)
* [Acknowledgments](preface/acknowledgments.md)

## Getting Started

* [Preface](<README (1).md>)
* [Armlab](getting-started/armlab/README.md)
  * [What is Armlab?](getting-started/armlab/background.md)
  * [Activating your Armlab Account](getting-started/armlab/activating-your-armlab-account.md)
  * [Logging into & out of Armlab](getting-started/armlab/logging-into-armlab/README.md)
    * [Secure Shell (SSH) Protocol](getting-started/armlab/logging-into-armlab/ssh-protocol.md)
  * [Configuring your armlab Environment](getting-started/armlab/configuring-your-armlab-environment.md)

## Fundamental Concepts

* [Linux and GNU](fundamental-concepts/linux-and-gnu.md)
* [Command Line Interface](fundamental-concepts/command-line-interface.md)
* [Terminal](fundamental-concepts/terminal.md)
* [Shell](fundamental-concepts/shell.md)
* [GNU Core Utilities](fundamental-concepts/gnu-core-utilities.md)
* [Operating System](fundamental-concepts/operating-system.md)
* [Putting it All Together](fundamental-concepts/putting-it-all-together.md)

## The Linux command line

* [What is Bash?](the-linux-command-line/background.md)
* [Getting Started](the-linux-command-line/warm-up-commands.md)
* [What commands represent](the-linux-command-line/what-commands-represent.md)
* [Command-line shortcuts](the-linux-command-line/useful-command-line-features.md)
* [Getting Help](the-linux-command-line/getting-help.md)
* [Navigating the filesystem](the-linux-command-line/navigating-the-filesystem/README.md)
  * [Printing Working Directory](the-linux-command-line/navigating-the-filesystem/pwd-print-working-directory.md)
  * [cd (Change Working Directory)](the-linux-command-line/navigating-the-filesystem/cd-change-working-directory.md)
  * [ls (List Directory Contents)](the-linux-command-line/navigating-the-filesystem/ls-list-directory-contents.md)
  * [Exercises](the-linux-command-line/navigating-the-filesystem/exercises.md)
* [Creating and Deleting Files and Directories](the-linux-command-line/creating-files-and-directories.md)
* [Viewing Files](the-linux-command-line/viewing-files.md)
* [Redirecting Input and Output](the-linux-command-line/redirection-and-piping.md)
* [Pipelines and Filters](the-linux-command-line/pipelines-and-filters.md)
* [Copying Files and Directories](the-linux-command-line/copying-files-and-directories/README.md)
  * [Moving and Renaming Files and Directories](the-linux-command-line/copying-files-and-directories/moving-and-renaming-files-and-directories.md)
* [Users Accounts](the-linux-command-line/users-and-groups.md)
* [File and Directory Access Permissions](the-linux-command-line/file-and-directory-access-permissions.md)
* [Bash Execution Environment](the-linux-command-line/bash-execution-environment.md)
* [Linux Filesystem](the-linux-command-line/filesystem/README.md)
  * [Files and Directories](the-linux-command-line/filesystem/files-and-directories.md)
  * [Filenames](the-linux-command-line/filesystem/filenames.md)
  * [Filesystem Layout](the-linux-command-line/filesystem/filesystem-layout.md)
  * [Notable Directories](the-linux-command-line/filesystem/notable-directories.md)
  * [Pathnames](the-linux-command-line/filesystem/pathnames.md)
* [Bash Cheat Sheet](the-linux-command-line/bash-cheat-sheet.md)
* [Further Reading](the-linux-command-line/further-reading.md)

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

## Git

* [Introduction](git/background/README.md)
  * [Setting Up Your Git/GitHub Environment](git/background/git-installation.md)
  * [GitHub](git/background/github/README.md)
    * [Authentication](git/background/github/authentication.md)
* [The big picture](git/the-big-picture.md)
* [Git Workflow](git/acquiring-a-git-repository.md)
* [Getting Help](git/getting-help.md)
* [Pushing and Pulling](git/pushing-and-pulling.md)
* [Obtaining COS217 Assignment Repositories](git/acquiring-cos217-assignment-repositories.md)
* [COS217 Development Workflow](git/cos217-development-workflow.md)
* [Revisiting add, commit, push, and pull](git/git-workflow-1/README.md)
  * [git add](git/git-workflow-1/staging-files.md)
  * [git commit](git/git-workflow-1/committing-staged-files.md)
  * [git push](git/git-workflow-1/pushing-commits.md)
  * [git pull](git/git-workflow-1/git-pull.md)
* [Important Git commands](git/important-git-commands/README.md)
  * [Checking the Status of Your Repository](git/important-git-commands/checking-the-status-of-your-repository.md)
  * [Viewing Commit History](git/important-git-commands/viewing-commit-history.md)
  * [Ignoring Files](git/important-git-commands/ignoring-files.md)
* [Branching](git/branching.md)
* [Resolving Merge Conflicts](git/resolving-merge-conflicts.md)
* [Configurations](git/configurations.md)
* [Git Cheatsheet](git/git-cheat-sheet.md)
* [Further Reading](git/further-reading.md)

## GCC Build Process

* [Introduction](gnu-compiler-collection-gcc/introduction.md)
* [An Overview of the Build Process](copy-of-gnu-compiler-collection-gcc/the-four-stage-build-process/README.md)
* [Important GCC Commands](gcc-build-process/important-gcc-commands.md)
* [Example](gcc/page-1.md)
* [Identifying Build Errors](gcc/identifying-build-errors.md)
* [GCC Cheatsheet](gnu-compiler-collection-gcc/gcc-cheatsheet.md)
* [Further Reading](copy-of-gnu-compiler-collection-gcc/further-reading.md)

## Make

* [Introduction](make/introduction.md)
* [Motivation For Make](make/background.md)
* [Makefile](make/makefiles/README.md)
  * [Writing a Makefile](make/makefiles/makefile-version-1-basic.md)
  * [Phony targets](make/makefiles/makefile-version-2-phony-targets.md)
  * [Macros](make/makefiles/makefile-version-3-macros.md)

## Gprof

* [Background](gprof/background.md)
* [How Gprof Works](gprof/how-gprof-works.md)
* [Using Gprof](gprof/using-gprof.md)
* [Interpreting Gprof Output](gprof/interpreting-gprof-output.md)
  * [Flat Profile](gprof/interpreting-gprof-output/flat-profile.md)
  * [Call Graph](gprof/interpreting-gprof-output/call-graph.md)

## Appendices

* [Appendix B: Detailed Explanation of I/O and Redirection & Piping](appendices/detailed-explanation-of-i-o-and-redirection-and-piping.md)
* [Assembly](appendices/assembly.md)
* [High Level Programming Language](appendices/high-level-programming-language.md)
* [Executable files](appendices/executable-files.md)
* [Further Reading](appendices/further-reading.md)
* [Machine Code](appendices/machine-code.md)
* [How Information is Represented in Computers](appendices/how-information-is-represented-in-computers.md)
* [C Preprocessor](appendices/c-preprocessor.md)
* [How Bash Executes Cammands](appendices/how-bash-executes-cammands/README.md)
  * [Path Environment Variable](appendices/how-bash-executes-cammands/path-environment-variable.md)
* [gcc extra](appendices/gcc-extra.md)

## Group 1

* [Glossary](appendices/glossary.md)

## GCC version 2

* [Page 1](gcc-version-2/page-1.md)
