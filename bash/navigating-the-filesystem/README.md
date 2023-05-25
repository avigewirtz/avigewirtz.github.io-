# Navigating the filesystem

To navigate the Linux filesystem, you need only be familiar with three commands: _pwd_, _ls_, and _cd_. These commands are perhaps the most commonly used Bash, so it is worth your while to make the extra effort to master them.&#x20;

To navigate to a directory, you must specify its [pathname](../../linux/filesystem/pathnames.md)--either absolute or relative. The choice between the two is typically a matter of preference or convenience.&#x20;

When using an absolute pathname to navigate, your working directory's current location is irrelevant. This is because an absolute pathname always point to the same location, irrespective of your current working directory. As an analogy, imagine giving someone directions from Times Square to Princeton - you need not be aware of the person's current location, as it has no bearing on the directions.&#x20;

Conversely, when using a relative pathname to navigate, your working directory's current location is significant - it's your starting point. In the previous analogy, imagine giving directions from the person's current location to Princeton. To do this, you would need to know where they are starting from. This is similar to using relative pathnames.

### Example: Navigating to _/usr/bin_&#x20;

As a practical example, say you're logged into Armlab and want to navigate to _/usr/bin._&#x20;

#### Method 1: Navigating with an absolute pathname

Using the absolute pathname, your working directory's "location" is inconsequential, since the "journey" always begins at the root directory. As such, you'd simply specify the path as _/usr/bin_, as shown in Figure 1. &#x20;

<figure><img src="https://lh6.googleusercontent.com/fsuhMi2igXx5_uDBRqn13MQUrJi4ksQEh30Tdq7jU5n3nU3UeUPB1lQD2qJqX9DNqztHBgPh27yVLONYOe8Gxuub6Sc3diq8ix8xNczgqBvq_faelUp2N6ybmdcqWoWyEgqJc6YJXfFLkOpM7cabdr0" alt=""><figcaption><p>Figure 1: Navigating to <em>/usr/bin</em> with Absolute Pathname</p></figcaption></figure>

#### Method 2: Navigating with a relative pathname

Conversely, when navigating to _/usr/bin_ with a relative pathname, you need to be aware of the "location" of your current working directory. Figure 2 demonstrates the pathname from the working directory to _/usr/bin_.

<figure><img src="https://lh5.googleusercontent.com/FraWHki7SFmGbu8SBMKFuNxOKUKnujwUXhvGMeizYJB_CtG1Qcmh5lv-yeXghuSxeojlmpn1i-4pjrtnaBBQT20dXztNWHNvIreerEt0iZNMHNXtFhBifxYGM2G3Vn2NhKZK0yu8A_Gayw6J3SPAQ4Q" alt=""><figcaption></figcaption></figure>
