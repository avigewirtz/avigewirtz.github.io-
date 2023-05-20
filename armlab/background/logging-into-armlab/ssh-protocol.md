# SSH Protocol

## What even is a protocol?



Secure Shell (SSH) is a protocol that provides a secure way to access a remote computer. It's primarily used to login to a remote computer and execute commands. SSH uses the Client-server model, connecting an SSH client instance with an SSH server.

1. Establishing a Connection: When you want to connect to another computer (the "remote" computer), you use a software application (an "SSH client") to make that request. Your computer is the "local" computer.
2. Authentication: The remote computer verifies your identity before it opens up a connection. This is often done using a username/password combination, although a more secure method is to use a pair of digital keys (one private, one public).
4. Encryption: Once your identity is confirmed and a connection is established, SSH then provides strong encryption for your session. Any data you send over the connection is encrypted on your local computer first, then sent to the remote computer where it's decrypted. This way, even if someone manages to intercept the data while it's in transit, they can't read it because it's encrypted.
5. Integrity and Confidentiality: SSH also ensures that no one has tampered with the data while it was in transit, and it keeps your session confidential. If the data was changed in transit, the receiving computer would know.
6. Command Execution: Once the secure connection is established, you can execute commands on the remote computer from your local machine as if you were sitting right in front of it. 