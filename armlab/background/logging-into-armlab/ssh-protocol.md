# Secure Shell (SSH) Protocol

Secure Shell (SSH) is a network protocol that provides an encrypted communication channel between two physically distant computers. Its primary function is to enable logging into a remote computer and executing commands.H

### SSH Architecture

SSH operates on the client-server model, connecting an instance of an SSH client with an instance of an SSH server. Note that these programs are distinct from the SSH protocol itself. The SSH protocol defines the rules for secure communication, while software tools like OpenSSH, PuTTY, and others implement these rules in their unique ways.

### Key Features of SSH

Authentication: Before establishing a connection, the remote computer authenticates your identity using a username/password combination or a digital key pair (one private, one public). Encryption: Once your identity is authenticated and a connection is established, SSH provides strong encryption for your session. Any data sent over the connection is encrypted on your local computer and decrypted on the remote one. This ensures that even if the data is intercepted during transmission, it cannot be read as it is encrypted. Integrity: SSH not only maintains the confidentiality of your data but also protects the integrity of data transmissions. If any data is altered during transmission, the SSH server on the receiving end can detect such alterations.
