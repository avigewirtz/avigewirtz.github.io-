# Introduction

Managing projects as a beginner often involves saving multiple versions of files directly on your computer or in basic cloud storage. You might name your files descriptively (e.g., "project\_v1," "project\_v2") to keep track of your progress. While this method is simple and requires no special tools, it has limitations as your projects become more complex.

Imagine having dozens of file versions or multiple people trying to work on the same project simultaneously. It quickly becomes messy and hard to manage. That's where a version control system (VCS) like Git comes in. Furthermore, manually managing all files severely complicates basic synchronization, especially when multiple people collaborate on the same project. Coordination becomes cumbersome if each team member must manually distribute their updates to others.

**What is Version Control?**

Version control systems are designed to solve the challenges of manual file management in software development. Two use cases: private and team. Key benefits include:

* Examine the state of your project at earlier points in time
* Show the differences among various states of the project
* Split the project development into multiple independent lines, called “branches,” which can evolve separately&#x20;
* Periodically recombine branches in a process called “merg‐ ing,” reconciling the changes made in two or more branches.&#x20;
* Allow many people to work on a project simultaneously, sharing and combining their work as needed
* **Change tracking and history:** VCS keeps a detailed history of all changes made to your project files. You can easily see who made changes, what they changed, and when.
* **Reversing changes:** If something goes wrong, you can quickly revert to a previous, working version of your code.
* **Collaboration:** Multiple people can work on the same project simultaneously without overwriting each other's work. Changes get merged in a controlled manner.
* **Branching:** Create separate development paths (branches) to work on new features or fixes in parallel. Later, these branches are merged back into the main project. In one branch, we might focus on a new feature, while another branch could be dedicated to bug fixes. Upon completion, these branches are merged, integrating the new feature with the bug fixes into a singular code version.
* Ownership tracking. aka blame. A nearly insurmountable challenge is tracking the so-called ownership of the code—identifying who made specific changes, when they made them, and why. This information is often crucial.&#x20;

...and much more.

**Git**

Git is a free, open-source, distributed version control system created by Linus Torvalds. It's incredibly popular and has become an essential tool for software development. With Git, you keep a complete history of your project files in a centralized place called a repository.
