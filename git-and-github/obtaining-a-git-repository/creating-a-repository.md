# Creating a Repository

The process of creating a Git repository is extremely simple. You simply navigate to the directory whose contents you want to version control and invoke `git init`. For example, to create a Git repository in the directory _\~/my\_project_, you'd invoke these two commands:

```bash
# navigate to my-project
cd ~/my_project 
# create the Git repository
git init 
```

Upon execution of these commands, _my\_project_ will be populated with a _.git_ directory, which contains the Git repository. Note that .git is a hidden directory, so it will only be visible when `ls` is invoked with the `-a` option (i.e., `ls -a`).
