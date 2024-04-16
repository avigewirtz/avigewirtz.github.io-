# cloning

## Repositories can be copied

Instead of initliazing a repository from sctrach, you can clone an existing repository. for example, in cos217, you copy repository's from cos217 GItHub account.&#x20;

The process of cloning a repository is extremely straightforward as well. You simply navigate to the directory you want the clone to reside in and invoke `git clone` with the source repository's URL as an argument. A GitHub URL has the following format:

```
https://github.com/GITHUB_USERNAME/REPOSITORY_NAME.git
```

GITHUB\_USERNAME represents the username of the GitHub account you are cloning from, and REPOSITORY\_NAME represents the name of the source repository. For example, if you're cloning the Survey repository from the COS217 GitHub account, you'd replace GITHUB\_USERNAME with cos217 and REPOSITORY\_NAME with _survey_:

```bash
git clone https://github.com/cos217/survey.git 
```

Upon success, you will get the following output:
