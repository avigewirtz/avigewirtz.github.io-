# Cloning a Repository

The process of cloning a repository is extremely straightforward as well. You simply navigate to the directory you want the clone to reside in and invoke `git clone` with the source repository's URL as an argument. A GitHub URL has the following format:

```
https://github.com/GITHUB_USERNAME/REPOSITORY_NAME.git
```

GITHUB\_USERNAME represents the username of the GitHub account you are cloning from, and REPOSITORY\_NAME represents the name of the source repository. For example, if you're cloning the assignment 0 Survey repository from the COS217 GitHub account, you'd replace GITHUB\_USERNAME with cos\_217\_ and REPOSITORY\_NAME with _survey_:

```bash
git clone https://github.com/cos217/survey.git 
```

Upon success, you will get the following output:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-04 at 8.00.49 PM (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Note that the arguments for the GitHub account and repository names are case-insensitive--that is, COS217, cos217, and Cos217 all refer to the same GitHub account (and the same applies to variations of _survey_).
