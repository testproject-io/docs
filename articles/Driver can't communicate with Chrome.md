---
description: What to do if the agent can't communicate with the requested browser.
---

# Driver can't communicate with Chrome

If you're executing a test on Chrome and seeing the following error message:

```
Failed communicating with the requested browser.
Please check your network settings.
```

You may want to check that your PC's hosts file includes an entry for localhost.

Chrome communicates via localhost, and if the entry is missing, it will crash during execution.

The hosts file is located in:

_**Windows**_

_c:\windows\system32\drivers\etc\hosts_

_**MacOS and Linux**_

_/etc/hosts_

Note that the file needs to be **opened as an administrator** to be edited.

After opening the file, check that you have the following line, if not simply add it:

`127.0.0.1 localhost`
