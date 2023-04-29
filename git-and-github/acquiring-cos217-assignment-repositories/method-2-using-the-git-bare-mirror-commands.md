# Method 2: Using the Git bare/mirror commands

The second method is somewhat complicated and  involves many more steps than the first method; however, this process can be used for any Git repository (without the need to use GitHub), so it is worth mentioning. The steps are as follows:



1. Clone the COS217 GitHub repository to your development computer.&#x20;
2. Create a new repository on GitHub.&#x20;
3. Upload the data from your local copy to your repository on GitHub.&#x20;
4. Clone your (updated) GitHub repository to your development computer&#x20;
5. (Optional) delete the bare clone&#x20;

The precise meaning behind all the Git commands to follow is beyond the scope of 217. However, in short, this convoluted sequence is necessary to obtain a copy that is completely independent of the source repository. If you were to do a stadaring (non bare) clone, your local copy would be linked to the official COS217 repository, which is not what you want. You want it to be linked to your personal GitHub copy.&#x20;

\
\
