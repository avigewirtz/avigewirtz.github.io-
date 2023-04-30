# Background

## Git

Git is a popular version control system (VCS). It was originally authored by Linus Torvalds, the founder of the Linux operating system, to manage the Linux kernel's source code. Before delving into the specifics of Git, it is essential to first understand the concept of version control and its significance in the software development process.&#x20;

## Motivation

In both team-based and large-scale single-developer programming projects, it is crucial to keep track of all material changes to the codebase. Maintaining such a record provides the capability to revert to a previous version when necessary.&#x20;

The most basic approach involves duplicating a codebase on the local filesystem each time a snapshot of its current version is desired. Although this method is reasonably effective for small projects, it rapidly becomes unwieldy and error-prone as projects grow in size.&#x20;

To seamlessly track and manage changes to a codebase over time, developers utilize VCS software. Some benefits of VCS include:

1. Reverting a codebase to a prior state. This is useful in many situations; for example, when a modification introduces a bug.&#x20;
2. Keeping a record of modifications to a codebase over time. This enables developers to pinpoint when specific features were added, deleted, or altered.
3. Creating and maintaining separate copies of the codebase. This allows developers to experiment and test new features without jeopardizing the original codebase’s stability.

## GitHub

GitHub is an online platform that hosts Git repositories. Starter code, data, and tools for COS 217 assignments are stored in repositories hosted on GitHub as part of the COS 217 GitHub organization

## Git vs. GitHub

&#x20;While Git and GitHub are closely associated with each other, it is important to understand that they are two distinct entities.&#x20;

A few key differences between them:

1. Git is an open-source software maintained by GNU; Github is a web-based platform owned by Microsoft.
2. Git is a VCS, while GitHub is a platform that (primarily) hosts Git repositories. &#x20;
3. Git is stored locally and can be accessed without an Internet connection; Github is stored on Microsoft servers and requires an Internet connection to access.&#x20;
4. While Git primarily focuses on version control, GitHub extends its capabilities by offering additional features such as enhanced project collaboration, project management, and code review.

In summary, Git is the underlying version control system used to manage repositories, while GitHub is an online platform that hosts Git repositories and provides tools for collaborative software development.
