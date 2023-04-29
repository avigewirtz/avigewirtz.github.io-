# Setting Up Your Environment

### Installing Git

In COS217, there is actually no need to install Git on your personal computer, since you can (and should) do all of your development on armlab, which already has Git installed.&#x20;

If you insist on developing with your personal computer, you can refer to Appendix A for Git installation instructions. Keep in mind that you will need to transfer the assignment files from your personal computer to Armlab for submission. Be aware that working on your personal computer is not advised, as the software versions or configurations on Armlab may differ from those on your computer, potentially leading to discrepancies when testing your code.

### Creating a GitHub Account

GitHub offers both free and paid accounts. For the purposes of COS217, a free GitHub account is sufficient. To create your account, go to [github.com](https://github.com/), click `Sign up` in the top-right corner, and follow the instructions.&#x20;

### Generating a GitHub Personal Access Token&#x20;

When authenticating with GitHub via the command line, GitHub requires you to use a **Personal Access Token** (PAT) instead of your account password.&#x20;

To generate a PAT, follow these steps:

1. Sign in to your [GitHub](https://github.com/) account.&#x20;
2. Click your profile picture in the top-right corner of the page and select `Settings` from the dropdown menu.
3. Scroll down to the bottom of the left sidebar in the `Settings` page and click on `Developer settings`.
4. Navigate to the bottom of the left sidebar and click `Personal access tokens`. In the resulting dropdown, click `Tokens (classic)`.
5. Click `Generate a personal access token`.
   * Check the ‘repo’ scope box.&#x20;
6. Click the `Generate token` button at the bottom of the page.

Your new PAT will be displayed. Be sure to copy it immediately, as GitHub will not show it again. Store it securely and treat it like a password. If you ever lose your PAT, do not worry. Simply generate a new one by following the steps above.

{% hint style="info" %}
Optional but strongly recommended: You will very quickly tire of copying and pasting your PAT each time you pull or push. You can use your computer’s keychain or password service to save your credentials, or you can use the Git client itself by configuring it using this command:

```bash
git config --global credential.helper store
```

This creates a file in your home directory that only you can access that contains your GitHub username and PAT, which will be read by Git during subsequent commands. This eliminates the need to enter your credentials manually in future Git operations
{% endhint %}



\
\
