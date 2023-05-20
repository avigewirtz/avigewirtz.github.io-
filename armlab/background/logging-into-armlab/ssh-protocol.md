# Secure Shell (SSH)

Secure Shell (SSH) is a cryptographic netwrok protocol that provides a secure way to access a remote computer. It's primarily used to login to a remote computer and execute commands. 

To better understand SSH, one needs to grasp the concept of a protocol. In the realm of computing and networking, a protocol is a set of rules or conventions that dictate how data is transmitted and exchanged across a network. These rules might cover aspects such as error checking, data compression, and packet sequencing, as well as data security and integrity. Essentially, a protocol serves as a kind of "language" that devices use to communicate and comprehend each other.

Note that a protocol is distinct from an SSH program. The protocal defines the rules while the program its implementation. The protocol establishes the communication rules, while the program implements the rules. Numerous implementations can adhere to the same protocol but might be written in different programming languages, utilize different algorithms, or offer unique features. This principle applies to SSH, which has many distinct software tools implementing the SSH protocol, such as OpenSSH, PuTTY, and others. Each of these tools complies with the rules of the SSH protocol while also having unique characteristics.

## SSH architecture 

SSH uses the client-server model, connecting an SSH client instance with an SSH server. The primary features SSH provides are authentication, encryption, and data integrity. This can be illustration with the following sequence:

1. Establishing a Connection: When you want to connect to another computer (the "remote" computer), you use a software application (an "SSH client") to make that request. Your computer is the "local" computer.
2. Authentication: The remote computer verifies your identity before it opens up a connection. This is often done using a username/password combination, although a more secure method is to use a pair of digital keys (one private, one public).
4. Encryption: Once your identity is confirmed and a connection is established, SSH then provides strong encryption for your session. Any data you send over the connection is encrypted on your local computer first, then sent to the remote computer where it's decrypted. This way, even if someone manages to intercept the data while it's in transit, they can't read it because it's encrypted.
5. Integrity: SSH also ensures that no one has tampered with the data while it was in transit, and it keeps your session confidential. If the data was changed in transit, the receiving computer would know.
6. Command Execution: Once the secure connection is established, you can execute commands on the remote computer from your local machine as if you were sitting right in front of it. 