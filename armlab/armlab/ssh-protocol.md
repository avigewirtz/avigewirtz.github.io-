# Secure Shell (SSH) Protocol

SSH is a protocol that provides an encrypted communication channel between two computers over a network. Its primary function is to enable users to log into a remote computer and execute commands.

#### SSH Architecture

SSH operates on a client-server model. An SSH client program, such as `ssh`, connects to a SSH server program, such as `sshd`, which relays commands to the local shell (e.g., bash) and sends the output back to the client.

#### Key Security Features of SSH

**Authentication**: Before establishing a connection, the SSH server authenticates your identity by prompting you for a username/password or by using a digital key pair (one private, one public).

**Encryption**: Once your identity is authenticated and a connection is established, SSH provides strong encryption for your session. Any data sent over the connection is encrypted. This ensures that even if the data is intercepted during transmission, it cannot be read.

**Data integrity**: SSH not only maintains the confidentiality of data but also protects its integrity. If any data is altered during transmission, the SSH program on the other end can detect it.
