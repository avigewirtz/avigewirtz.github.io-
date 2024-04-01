# Exercises

For the following questions, unless otherwise stated, assume the working directory is /u/yourNetID.

1. Which of the following commands will list the contents of your current working directory in a detailed format, including hidden files?
   * A) `ls -a`
   * B) `ls -l`
   * C) `ls -la`
   * D) `ls -lh`
2. What does `cd ..` achieve?
   * A) It moves you up one directory from your current location
   * B) It takess you to your home directory
   * C) It takes you to the root directory
   * D) It does nothing
3. What happens if you attempt to change your working directory to another user's home directory, such as `/u/bwk`?
   * A) The command succeeds without any issue
   * B) You are prompted for the other user's password
   * C) The command fails due to permissions, unless you have explicit permissions
   * D) Your current directory is unchanged, and an error message is displayed
4. Which of the following lists the contents of the root (/) directory?
   * A) `ls /`
   * B) `cd /` then `ls`
   * C) `pwd /`
   * D) `ls -root`
5. How do you return to the last directory you were in?
   * A) `cd ..`
   * B) `cd -`
   * C) `cd ~`
   * D) `cd /`
6. If you are in `/u/yourNetID`, what command takes you directly to your home directory?
   * A) `cd`
   * B) `cd ~`
   * C) `cd /u/yourNetID`
   * D) Both A and B
7. How do you change your working directory to `/usr/bin` from anywhere in the filesystem?
   * A) `ls /usr/bin`
   * B) `pwd /usr/bin`
   * C) `cd /usr/bin`
   * D) `dir /usr/bin`
8. What does the `pwd` command output?
   * A) List of files in the current directory
   * B) The current working directory's absolute path
   * C) The user's home directory path
   * D) The contents of a specified directory
9. Which of the following commands lists the contents of the working directory in long format?
   * A) `ls -l`
   * B) `pwd -l`
   * C) `cd -l`
   * D) `ls --long`
10. You're in `/home/username` and attempt to `cd` into a file named `notes.txt` in your current directory. What happens?
    * A) The file `notes.txt` opens in the default text editor
    * B) The terminal displays an error message
    * C) The command is successful, and `notes.txt` becomes the current directory
    * D) The command deletes `notes.txt`
11. From `/home/username/documents`, how do you navigate to `/home/username` using `cd`?
    * A) `cd /home/username` using absolute path
    * B) `cd ..` using relative path
    * C) Both A and B are correct
    * D) `cd ~/documents`
12. If your current working directory is `/home/username`, how can you change it to `/usr/bin`?
    * A) `cd /usr/bin`
    * B) `cd ../../usr/bin` assuming `/home/username` is your starting point
    * C) `ls /usr/bin`
    * D) Both A and B are correct
13. What happens when you invoke cd ././././?
