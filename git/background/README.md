# Background

Git is a popular _Version Control System_ (VCS), originally authored by Linux founder Linus Torvalds to manage the Linux kernel's source code. Before delving into the specifics of Git, it is essential to first understand what version control is and its significance in the software development process.

## Version Control

In important software projects, it is crucial to keep track of all material changes made to the codebase over time. Maintaining such a record provides a safety net, enabling mistakes to be easily corrected by reverting to a previous version of the codebase.

The most basic approach involves duplicating a codebase on the local filesystem each time a snapshot of its current version is desired. Although this method is reasonably effective for small projects, it rapidly becomes unwieldy and error-prone as projects grow in size.

To seamlessly track and manage changes to a codebase over time, developers utilize VCS software. The most popular VCS software today is Git, which provides many benefits beyond simple version control. For example, it gives developers the ability to create and maintain separate copies of the codebase, allowing them to experiment and test new features without jeopardizing the original codebase’s stability. Additionally, it allows developers to seamlessly exchange data between repositories, enabling team members to efficiently collaborate on projects.

## GitHub

GitHub is an online platform that hosts Git repositories. The benefit of hosting repositories online is it makes them more accessible to others. The starter code and files for each COS217 assignment is uploaded as a Git repository on the COS 217 GitHub account.

## Git vs. GitHub

While Git and GitHub are closely associated with each other, it is important to understand that they are two distinct entities.

A few key differences between them:

1. Git is a VCS, while GitHub is a platform that (primarily) hosts Git repositories.
2. Git is a program that can be stored locally and accessed without an Internet connection; Github is a platform hosted on Microsoft servers that requires an Internet connection to access.
3. While Git primarily focuses on version control, GitHub extends its capabilities by offering additional features such as enhanced project collaboration, project management, and code review.
4. Git is an open-source software project maintained by GNU; Github is a web-based platform owned by Microsoft.

In summary, Git is the underlying version control system used to manage repositories, while GitHub is an online platform that hosts Git repositories and provides additional tools for collaboration.
