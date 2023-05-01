# Navigating the filesystem

When you log into a Linux system, your working directory is by default your home directory. Unless you are a system administrator, you will rarely need to navigate to directories above your home directory; you will, however, regularly need to navigate to directories below it. To navigate to a directory, you must specify its pathname. As a refresher, each directory has two types of pathnames: absolute and relative. A directory’s absolute pathname specifies its location in the directory hierarchy by tracing its path from the root directory, while a directory’s relative pathname specifies its location by tracing its path from the working directory.&#x20;

To navigate the directory hierarchy seamlessly, it’s helpful to have a visual perception of the distinction between absolute and relative pathnames. As a practical example, in the filesystem snapshot shown in Figure 1, say you want to navigate to _bin_ (circled in red).

<figure><img src="https://lh5.googleusercontent.com/zhvz5mD3xu6o89CUIY3hJJkuab6SMH2xkwIXWL8k_gIhYGLCLTO6l8xSj8Vfb2BKycdrFo66aZgKgJhTP60Z2IvCJPtrCVNt214VY_0mAH5H1FdsmEl3pDKMwM1c4PKfGTBSZ2nmlDTdP1AxbfMtWL8" alt=""><figcaption></figcaption></figure>

The first to accomplish this is by specifying bin’s absolute pathname, as shown in Figure 2. In such a case, it makes no difference what your working directory is, since absolute pathnames always take you to the same location, irrespective of your working directory.&#x20;

<figure><img src="https://lh6.googleusercontent.com/fsuhMi2igXx5_uDBRqn13MQUrJi4ksQEh30Tdq7jU5n3nU3UeUPB1lQD2qJqX9DNqztHBgPh27yVLONYOe8Gxuub6Sc3diq8ix8xNczgqBvq_faelUp2N6ybmdcqWoWyEgqJc6YJXfFLkOpM7cabdr0" alt=""><figcaption></figcaption></figure>

The second way is by specifying bin’s relative pathname, as shown in Figure 3.&#x20;

<figure><img src="https://lh5.googleusercontent.com/FraWHki7SFmGbu8SBMKFuNxOKUKnujwUXhvGMeizYJB_CtG1Qcmh5lv-yeXghuSxeojlmpn1i-4pjrtnaBBQT20dXztNWHNvIreerEt0iZNMHNXtFhBifxYGM2G3Vn2NhKZK0yu8A_Gayw6J3SPAQ4Q" alt=""><figcaption></figcaption></figure>

### Bash commands to navigate to filesystem

To navigate the Linux filesystem, you need only be familiar with three commands: pwd, ls, and cd. These commands are perhaps the most popular Linux commands and are invoked in just about every terminal session; thus, it is worth your while to pay particular attention to them and make the effort to master them. The extra time spent now will be miniscule compared to the time saved later.&#x20;
