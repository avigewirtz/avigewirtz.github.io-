# Recording changes to repository

Now that we understand how the index works, we're in a better position to explain how

## Modifying the working tree <a href="#checking_status" id="checking_status"></a>

At this point, if we invoke git status, it'll tell us that our working tree is "clean":

<figure><img src="../../.gitbook/assets/Screenshot 2024-04-04 at 5.10.37 PM.png" alt=""><figcaption></figcaption></figure>

A clean working tree means that our working tree does not contain any new, modified or deleted files. In Git terminology, all the files in our working tree are "unmodified."&#x20;

if anything changes and we want to apply the changes, we will have to add the changes to the index. These modifications include:

* Creating a new file
* Modifying an existing file
* Deleting a file

Let's now make all three modifications to our working. First, let's modify hello.txt by appending "world" to it:

```
echo "world" >> hello.txt
```

Next, let's create a new file named hey.txt, and write "hey" in it:

```
echo "hey" >> hey.txt
```

finally, let's delete the file hi.txt:

```
rm -rf hi.txt
```

Invokig git status, we see that hello.txt is listed as modified, hey.txt as untracked, and hi.txt.&#x20;

Let's now examine the state of our working tree with Git status:&#x20;





The output tells us two things:

1. hello.txt was modified, and the modified version is not staged for commit.&#x20;
2. hey.txt is untracked











A perhaps pedantic but subtle point. Notice how we didn't have to add the unmodified files--hi.txt and bye.txt--to the staging area. We only had to stage hello.txt. This is because unmodified files are automatically in the staging area. This is a subtle point but will. When we invoke git status, it only lists the changes, but not unmodifies files.&#x20;



We see that the newly added file hey.txt is listed as "untracked." What happens is, git looks at the index, and sees no file with the name "hey.txt". (This is different that the previous example of. If a file is not in the index, then then not only is it not part of a previous commit, Git does not even track it. was it never part of In simple terms, an untracked file is one that is not in the staging area.  As we'll see soon, if you modify or delete an untracked file, Git won't&#x20;





{% hint style="info" %}
## When to commit



When working on your own, it’s useful to commit “early and often,” so that you can explore different ideas and make changes freely without worrying about recovering earlier work. Such commits are likely to be somewhat disorganized and have cryptic commit messages, which is fine because they need to be intelligible only to you, and for a short period of time. Once a portion of your work is finished and you’re ready to share it with others, though, you may want to reorganize those commits, to make them well-factored with regard to reusability of the changes being made (especially with software), and to give them mean‐ ingful, well-written commit messages.

The timing for creating commits is up to you, but it's a good practice to commit whenever you've completed a logical chunk of work. For example, if you've implemented a new feature, tested it, and everything works, that's an ideal time to commit. Remember, it's usually better to have smaller, focused commits rather than massive ones that try to cram in many unrelated changes.
{% endhint %}

###

<figure><img src="../../.gitbook/assets/image (7) (1) (1).png" alt=""><figcaption></figcaption></figure>

