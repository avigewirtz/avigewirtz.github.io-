# Armlab

Armlab is a Linux-based computer cluster maintained by Princeton's Computer Science department. The cluster consists of two interconnected computers—armlab01 and armlab02.

As a student in COS217, you are assigned a user account on Armlab, which you'll use to develop and submit your C and assembly programs. The purpose of Armlab in CO217 is to ensure a standardized computing environment for everyone in the course.

To access Armlab, you log in from your personal computer by establishing an SSH connection over a network. The instructions for doing so are provided in [Logging Into Armlab](logging-into-armlab.md#logging-into-armlab). While you work on Armlab, Linux provides the illusion that you're the only user on the system. In reality, however, many users may be logged in concurrently (Figure 1). Armlab runs on something of the order of 96 CPUs, so it has no problem handling many users.



<figure><img src="../../.gitbook/assets/Group 12 (1) (1).png" alt=""><figcaption><p>Figure 1: Concurrent SSH Sessions with Armlab</p></figcaption></figure>