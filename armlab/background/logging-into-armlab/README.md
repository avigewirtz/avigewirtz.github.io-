# Logging into & out of Armlab

## Logging into Armlab

Logging into Armlab is accomplished via an _SSH client,_ which is a program that uses the [SSH](ssh-protocol.md) Protocol to communicate with a remote computer.H

{% tabs %}
{% tab title="Mac" %}
On macOS, you can connect to armlab via Terminal by invoking the _ssh_ command.

1. Open Terminal and enter the following command:

<pre class="language-bash"><code class="lang-bash">ssh <a data-footnote-ref href="#user-content-fn-1">YOUR_NETID</a>@armlab.cs.princeton.edu
</code></pre>

{% hint style="info" %}
The first time you log into armlab, an SSH-related message will appear. Respond “yes”.
{% endhint %}

2. Input your Princeton password and authenticate your login credentials with DUO Security. (Note that your password will not be visible on the screen as you type it.)

If your login is successful, a shell prompt similar to the following will appear in your terminal window:

<figure><img src="../../../.gitbook/assets/Screenshot 2023-04-23 at 3.12.10 PM.png" alt=""><figcaption></figcaption></figure>

Note that the prompt may either state armlab01 or armlab02. These computers are interconnected and share the same filesystem, so it is inconsequential which one you are logged into.
{% endtab %}

{% tab title="Windows" %}
The PuTTY terminal emulator has a built-in SSH client.

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

<figure><img src="../../../.gitbook/assets/Screenshot 2023-04-23 at 3.12.10 PM.png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

## Logging out of armlab

to log out of armlab, simply invoke `logout`, and your terminal session will be closed.

<figure><img src="../../../.gitbook/assets/Screenshot 2023-05-09 at 3.44.12 PM.png" alt=""><figcaption></figcaption></figure>

[^1]: Replace with your real NetID.
