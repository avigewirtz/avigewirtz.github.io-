---
description: This page explains what armlab is, its role in COS217, and how it is accessed.
---

# Background

In COS217, armlab will serve as your primary platform for developing and executing your C and assembly programs. Armlab is a Linux-based computer cluster maintained by Princeton's Computer Science department. The cluster consists of two interconnected computers—armlab01 and armlab02.&#x20;

You can think of Armlab as a computer just like your own, but with a few notable differences::

1. Armlab is accessed remotely, rather than physically. Specifically, you log into Armlab from your personal computer by establishing an [SSH](logging-into-armlab/ssh-protocol.md) connection.&#x20;
2. Armlab is a multiuser computer utilized by hundreds of Princeton students and faculty, often concurrently.
3. Armlab runs on Linux (while your PC which likely runs on Windows or macOS). &#x20;

This idea is illustrated in Figure 1, which depicts multiple users logged into Armlab via SSH and using it concurrently.&#x20;

<figure><img src="../../.gitbook/assets/Group 12 (1) (1).png" alt="" width="563"><figcaption><p>Figure 1: Concurrent SSH Sessions in Armlab </p></figcaption></figure>

Before you can log into Armlab, you must first complete a couple of steps to [activate](activating-your-armlab-account.md) your account.
