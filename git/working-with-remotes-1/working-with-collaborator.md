# Working with collaborator







On the other hand, suppose another developer had already pushed some commits to the origin repository, and the result looked more like Figure 11-5 when you attemp‐ ted to push your history up to the origin repository. In effect, you are attempting to cause your history to be sent to the shared repository when there is already a different history there. The origin history does not simply fast-forward from B. This situation is called the non-fast-forward push problem.

When you attempt your push, Git rejects it and tells you about the conflict with a message like this:

$ git push\
To /tmp/Depot/my\_website

! \[rejected] main -> main (non-fast forward) error: failed to push some refs to '/tmp/Depot/my\_website'

So what are you really trying to do? Do you want to overwrite the other developer’s work, or do you want to incorporate both sets of histories?

If you want to overwrite all other changes, you can! Simply use the -f option on your git push. We just hope you won’t need that alternate history!

More often, you are not trying to wipe out the existing origin history but just want your own changes to be added. In this case, you must perform a merge of the two histories in your repository before pushing.
