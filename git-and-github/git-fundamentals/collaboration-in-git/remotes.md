# Remotes

As you can imagine, providing lengthy URLs everytime you wish to interact with a remote repository is tedious. Thus, to make things easier, Git can store the URLs of any number of remote repositories you are interested in names, or aliases, which are easier to remember.&#x20;

This way, you can interact with remote repositories through names, instead of URLs.

In fact, when you clone a Git repository, Git automatically stores the URL of the source repository in an alias named origin. Thus, after a clone operation, you can simply reference the source repository using “origin” instead of its URL.&#x20;

To simplify things further, Git defaults to origin whenever a remote isn’t supplied in a push or pull operation on the command line. Thus, a “git push/pull” is equivalent to git push/pull origin.&#x20;

Note that the relationship between a local and remote repository  is (by default) a one-way relationship. The remote repository has no knowledge of nor does it maintain a link to the local one.&#x20;
