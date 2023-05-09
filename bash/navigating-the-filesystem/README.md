# Navigating the filesystem

To navigate the Linux filesystem, you need only be familiar with three commands: _pwd_, _ls_, and _cd_. These commands are perhaps the most commonly used Bash, so it is worth your while to make the extra effort to master them.&#x20;

To navigate to a directory, you must specify its [pathname](../../linux/filesystem/pathnames.md)--either absolute or relative. The choice between the two is typically a matter of preference or convenience.&#x20;

### Navigating with Absolute Pathnames

When you navigate with a relative pathname, the current location of your working directory does not matter, since absolute pathnames always take you to the same location, irrespective of your working directory. You can think of it like someone asking you for directions from Times Square to Princeton. You can answer the question without knowing that person's current location, as the directions do not depend on that information.&#x20;

As a practical example, say you're logged into armlab and want to navigate to _/usr/bin._ If you navigate with its absolute pathname, you need not even be aware of the "location" of your working directory, since the "journey" begins at the root directory regardless, as demonstrated in the figure below.&#x20;

<figure><img src="https://lh6.googleusercontent.com/fsuhMi2igXx5_uDBRqn13MQUrJi4ksQEh30Tdq7jU5n3nU3UeUPB1lQD2qJqX9DNqztHBgPh27yVLONYOe8Gxuub6Sc3diq8ix8xNczgqBvq_faelUp2N6ybmdcqWoWyEgqJc6YJXfFLkOpM7cabdr0" alt=""><figcaption><p>Figure 1: Navigating to <em>/usr/bin</em> with Absolute Pathname</p></figcaption></figure>

### Navigating with Relative Pathnames

When you navigate with a relative pathname, you need to be aware of the "location" of your working directory, since that is where you "start" from. In our previous example, imagine that instead of asking you for directions from Times Square to Princeton, that person asked you for directions from their current location to Princeton. Of course, you would need to know their current location before you could provide directions. So too with relative pathnames. The figure below demonstrates navigating to _/usr/bin_ when your working directory is your home directory.

<figure><img src="https://lh5.googleusercontent.com/FraWHki7SFmGbu8SBMKFuNxOKUKnujwUXhvGMeizYJB_CtG1Qcmh5lv-yeXghuSxeojlmpn1i-4pjrtnaBBQT20dXztNWHNvIreerEt0iZNMHNXtFhBifxYGM2G3Vn2NhKZK0yu8A_Gayw6J3SPAQ4Q" alt=""><figcaption></figcaption></figure>
