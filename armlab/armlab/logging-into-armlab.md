# Logging Into and Out of Armlab

Logging into Armlab is accomplished via an _SSH client,_ which is a program that uses the [SSH Protocol](ssh-protocol.md) to communicate with a remote computer.

{% tabs %}
{% tab title="Mac" %}
On macOS, you can connect to Armlab via the Terminal application by using the _ssh_ utility.&#x20;

1. Open Terminal and enter the following command:

<pre class="language-bash"><code class="lang-bash">ssh <a data-footnote-ref href="#user-content-fn-1">YOUR_NETID</a>@armlab.cs.princeton.edu
</code></pre>

{% hint style="info" %}
The first time you log into Armlab, an SSH-related message will appear. Respond “yes”.
{% endhint %}

2. Input your Princeton password and authenticate your login credentials with DUO Security. (Note: Your password will not display on the screen as you type it.)

Assuming your login is successful, a shell prompt like the following will appear on your terminal window:

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-23 at 3.12.10 PM.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
The prompt will either state armlab01 or armlab02. These computers are interconnected and share the same filesystem, so it is inconsequential which one you are logged into.
{% endhint %}
{% endtab %}

{% tab title="Windows" %}
On Windows, logging into Armlab is done with PuTTY, which has a built in ssh client program.&#x20;

1. Launch PuTTY. Using Windows Explorer, double-click on the putty.exe file.
2. Click on the Window | Colours Category, and make sure the Use system colours checkbox is checked.
3. Click on the Session Category.
4. In the Host Name (or IP address) text box, type:\
   armlab.cs.princeton.edu
   * Make sure that the Port text box contains 22.
   * Make sure the Connection type radio button panel is set to SSH.
   * Make sure the Close window on exit radio button panel is set to Only on clean exit.
5. Click the Open button. If a PuTTY Security Alert dialog box appears, click Yes.
6. In response to _login as:_, enter your NetID. If an Access denied message appears, ignore it.\
   In response to the password: prompt, enter your Princeton password. (The password will not display as you type.)

If your login is successful, a shell prompt like the following will be displayed in your terminal window:

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-23 at 3.12.10 PM.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
The prompt will either state armlab01 or armlab02. These computers are interconnected and share the same filesystem, so it is inconsequential which one you are logged into.
{% endhint %}
{% endtab %}
{% endtabs %}

#### Logging out of Armlab

To log out of Armlab, simply invoke `logout`, and your terminal session will be closed:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-09 at 3.44.12 PM.png" alt=""><figcaption></figcaption></figure>

[^1]: Replace with your real NetID.
