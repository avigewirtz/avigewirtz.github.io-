# Secure Shell (SSH) Protocol

SSH is a protocol that provides an encrypted communication channel between two computers over a network. Its primary function is to enable logging into a remote computer and executing commands.

## SSH Architecture

SSH operates on the client-server model, connecting an instance of an _SSH client_ with an instance of an _SSH server_. An example of an ssh client is ssh program. An example of an ssh server is sshd.&#x20;

## Key Security Features of SSH

**Authentication**: Before establishing a connection, the remote computer authenticates your identity using a username/password combination or a digital key pair (one private, one public).&#x20;

**Encryption**: Once your identity is authenticated and a connection is established, SSH provides strong encryption for your session. Any data sent over the connection is encrypted on your local computer and decrypted on the remote one. This ensures that even if the data is intercepted during transmission, it cannot be read.&#x20;

**Data integrity**: SSH not only maintains the confidentiality of data but also protects its integrity during transmission. If any data is altered during transmission, the SSH server on the receiving end can detect it.
