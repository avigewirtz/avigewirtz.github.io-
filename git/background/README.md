# Introduction

Git is a free, open source, distributed version control system created by Linus Tor‐ valds.

Our goal in this book is to show you how to get the most out of Git and how to manage a Git repository with ease. By the end, you will have learned Git’s philosophy, fundamental concepts, and intermediate to advanced skills for tracking content, collaborating, and managing your projects across teams.







## About version control





When working on a software project, several tasks become really painful to do if we manage all the project files manually. The first is the ability to track and revert any changes made as we progress through different release cycles of our software. As we implement changes and address bugs, it would be highly beneficial if we could, when necessary, revisit old code or revert to an earlier version that did not contain a newly introduced bug.

Furthermore, manually managing all files severely complicates basic synchronization, especially when multiple people collaborate on the same project. Coordination becomes cumbersome if each team member must manually distribute their updates to others. A nearly insurmountable challenge is tracking the so-called ownership of the code—identifying who made specific changes, when they made them, and why. This information is often crucial. Additionally, manual file management hampers our ability to branch, that is, to diverge our work into different development paths. In one branch, we might focus on a new feature, while another branch could be dedicated to bug fixes. Upon completion, these branches are merged, integrating the new feature with the bug fixes into a singular code version. Attempting backups, change tracking and reverting, synchronization, ownership tracking, and branching manually is not only cumbersome but also prone to errors. Consequently, programmers resort to software tools known as Version Control Systems,  named for their primary function of tracking changes to the files and directories in our projects.

Git is a popular _Version Control System_ (VCS), originally authored by Linux founder Linus Torvalds to manage the Linux kernel's source code. Before delving into the specifics of Git, it is essential to first understand what version control is and its significance in the software development process.







The basic idea with git is you have a working tree with an associated repository. The working tree is simply the files of your project your working with. The repository is essentially the git database that keeps track of all changes to your project.&#x20;



There are two ways to obtain a git repository. The first is to create a new one for a project that's currently not under version control. The second is to copy, or clone in git teminology, an existing repository.&#x20;
