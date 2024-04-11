# Generating Personal Access Token (PAT)

When authenticating with GitHub via the command line, for security purposes GitHub requires you to use a _Personal Access Token (PAT)_ instead of your account password. To generate a PAT, follow these steps:

1. Sign into your [GitHub](https://github.com/) account.&#x20;
2. Click your profile picture in the top-right corner of the page and select **Settings** from the dropdown menu.
3. Scroll down to the bottom of the left sidebar and click **Developer settings**.
4. Navigate to the bottom of the left sidebar and click **Personal access tokens**. In the resulting dropdown menu, click **Tokens (classic)**.
5. Click **Generate a personal access token**.
   * Check the **repo** scope box.&#x20;
6. Click **Generate token** at the bottom of the page.

Your new PAT will be displayed. Be sure to copy it immediately, as GitHub will not show it again. Store it securely and treat it like a password. If you lose your PAT, you can simply generate a new one by following the above steps.

{% hint style="success" %}
**Optional but strongly recommended**: You will very quickly tire of copying and pasting your PAT to authenticate with GitHub. You can use your computer’s keychain or password service to save your credentials, or you can use the Git client itself by configuring it using this command:

```bash
git config --global credential.helper store
```

This creates a file in your home directory that only you can access that contains your GitHub username and PAT, which will be read by Git during subsequent commands. This eliminates the need to enter your credentials manually in future Git operations
{% endhint %}
