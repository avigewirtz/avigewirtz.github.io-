# Setting Up Your Git Environment

### Installing Git

In COS217, there is no need to install Git, since Git is already installed on Armlab. However, if you'd like to obtain Git on your PC as well, you can install it by following the instructions below.&#x20;

{% tabs %}
{% tab title="macOS" %}
There are many ways to install Git on macOS. The easiest method is by installing the _Xcode Command Line Tools._&#x20;

* Run the following command in Terminal: `git -v`. If Git is already installed, the command will output `git version X.Y.Z`. Otherwise, it will prompt you to install Xcode Command Line Tool, which includes a version of Git.

{% hint style="info" %}
Note that the version of Git included with Xcode is not necessarily the latest version. If you specifically want the latest version, download Git using the official Git [installer](https://git-scm.com/download/mac).&#x20;
{% endhint %}
{% endtab %}

{% tab title="Windows" %}
You may already have Git installed thanks to the introcs infrastructure from COS 126, which installs Git Bash. If this is not the case, navigate to http://git- scm.com/download/win, and the installation will start automatically.
{% endtab %}
{% endtabs %}

<details>

<summary>Creating a GitHub account</summary>

GitHub offers both free and paid accounts. For the purposes of COS217, a free GitHub account is sufficient. To create your account, go to [github.com](https://github.com/), click **Sign up** (top-right corner), and follow the instructions.&#x20;

</details>

<details>

<summary>Generating a GitHub personal access token (PAT)</summary>

When authenticating with GitHub via the command line, GitHub requires you to use a _Personal Access Token (PAT)_ instead of your account password. To generate a PAT, follow these steps:

1. Sign into your [GitHub](https://github.com/) account.&#x20;
2. Click your profile picture in the top-right corner of the page and select **Settings** from the dropdown menu.
3. Scroll down to the bottom of the left sidebar and click **Developer settings**.
4. Navigate to the bottom of the left sidebar and click **Personal access tokens**. In the resulting dropdown menu, click **Tokens (classic)**.
5. Click **Generate a personal access token**.
   * Check the **repo** scope box.&#x20;
6. Click **Generate token** at the bottom of the page.

Your new PAT will be displayed. Be sure to copy it immediately, as GitHub will not show it again. Store it securely and treat it like a password. If you ever lose your PAT, simply generate a new one by following the above steps.

Optional but strongly recommended: You will very quickly tire of copying and pasting your PAT to authenticate with GitHub. You can use your computer’s keychain or password service to save your credentials, or you can use the Git client itself by configuring it using this command:

```bash
git config --global credential.helper store
```

This creates a file in your home directory that only you can access that contains your GitHub username and PAT, which will be read by Git during subsequent commands. This eliminates the need to enter your credentials manually in future Git operations

</details>
