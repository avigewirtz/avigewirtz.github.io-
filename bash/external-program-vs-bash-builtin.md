# External Program vs bash builtin

Here are two methods you can use to determine if a command is a Bash built-in or a utility program.&#x20;

1. You can simply try `man` command, and if `man` succeeds, great. If not, Bash will return the following page, telling you that the command is a built-in:&#x20;

<figure><img src="https://lh4.googleusercontent.com/5k7q2Hl7hgogOQytiVUs5j1rgyHocnot1xIbIO-FFAaVkpOZy2e9Cm-APpoccvWTyjw1Yx6GCZCBydMULp9QvjzWFh1aB3tju7oNRUJktapPZwJzNMMycoWxH296Ez0BdCO_pjIz7TSszFff65CWH3g" alt="" width="563"><figcaption></figcaption></figure>

2. You can invoke `type` with the command name. For example, to check if the `exit` command is a Bash built-in, run:

<div align="left">

<figure><img src="../.gitbook/assets/Screenshot 2023-04-25 at 8.00.25 PM.png" alt=""><figcaption></figcaption></figure>

</div>

h
