# Goals of this tutorial

There are already several good books available on Git, including Scott Chacon’s Pro Git, and the full-size Version Control with Git by Jon Loeliger (O’Reilly). In addition, the Git software doc‐ umentation (“man pages” on Unix) is generally well written and complete. So, why a Git Pocket Guide? The primary goal of this book is to provide a compact, readable introduction to Git for the new user, as well as a reference to common commands and pro‐ cedures that will continue to be useful once you’ve already gotten some Git under your belt. The man pages are extensive and very detailed; sometimes, it’s difficult to peruse them for just the in‐ formation you need for simple operations, and you may need to refer to several different sections to pull together the pieces you need. The two books mentioned are similarly weighty tomes with a wealth of detail. This Pocket Guide is task oriented, organized around the basic functions you need from version control: mak‐ ing commits, fixing mistakes, merging, searching history, and so on. It also contains a streamlined technical introduction whose aim is to make sense of Git generally and facilitate understanding of the operations discussed, rather than completeness or depth for its own sake. The intent is to help you become productive with Git quickly and easily.

Since this book does not aim to be a complete reference to all of Git’s capabilities, there are Git commands and functions that we do not discuss. We often mention these omissions explicitly, but some are tacit. Several more advanced features are just mentioned

Preface | xi

and described briefly so that you’re aware of their existence, with a pointer to the relevant documentation. Also, the sections that cover specific commands usually do not list every possible option or mode of operation, but rather the most common or useful ones that fit into the discussion at hand. The goal is simplicity and economy of explanation, rather than exhaustive detail. We do provide frequent references to various portions of the Git docu‐ mentation, where you can find more complete information on the current topic. This book should be taken as an introduction, an aid to understanding, and a complement to the full documen‐ tation, rather than as a replacement for it.

At the time of this writing in early 2013, Git is undergoing rapid development; new versions appear regularly with new features and changes to existing ones, so expect that by the time you read this, some alterations will already have occurred; that’s just the nature of technical writing. This book describes Git as of version 1.8.2.









In this initial chapter, we discuss how Git operates, defining im‐ portant terms and concepts you should understand in order to use Git effectively.

Some tools and technologies lend themselves to a “black-box” approach, in which new users don’t pay too much attention to how a tool works under the hood. You concentrate first on learn‐ ing to manipulate the tool; the “why” and “how” can come later. Git’s particular design, however, is better served by the opposite approach, in that a number of fundamental internal design de‐ cisions are reflected directly in how you use it. By understanding up front and in reasonable detail several key points about its op‐ eration, you will be able to come up to speed with Git more quickly and confidently, and be better prepared to continue learning on your own.

Thus, I encourage you to take the time to read this chapter first, rather than just jump over it to the more tutorial, hands-on chap‐ ters that follow (most of which assume a basic grasp of the ma‐ terial presented here, in any case). You will probably find that your understanding and command of Git will grow more easily if you do.
