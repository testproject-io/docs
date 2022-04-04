---
description: Fix proxy issues when trying to work with remote agent on mobile devices
---

# Solving Proxy issues on Appium remote session

If you are experiencing an issue connecting to a remote machine via a proxy and running mobile tests that depend on Appium, and you get this error:

```log
[debug] [WD Proxy] Matched '/status' to command name 'getStatus'
[debug] [WD Proxy] Proxying [GET /status] to [GET http://127.0.0.1:53685/wd/hub/status] with no body
[WD Proxy] Got response with status 407: <HTML><HEAD>
[WD Proxy] <TITLE>Access Denied</TITLE>
[WD Proxy] </HEAD>
[WD Proxy] <BODY>
[WD Proxy] <FONT face="Helvetica">
[WD Proxy] <big><strong></strong></big><BR>
[WD Proxy] </FONT>
[WD Proxy] <blockquote>
[WD Proxy] <TABLE border=0 cellPadding=1 width="80%">
[WD Proxy] <TR><TD>
[WD Proxy] <FONT face="Helvetica">
[WD Proxy] <big>Access Denied (authentication_failed)</big>
[WD Proxy] <BR>
[WD Proxy] <BR>
[WD Proxy] </FONT>
[WD Proxy] </TD></TR>
[WD Proxy] <TR><TD>
[WD Proxy] <FONT face="Helvetica">
[WD Proxy] Your credentials could not be authenticated: "Credentials are missing.". You will not be permitted access until your credentials can be verified.
[WD Proxy] </FONT>
[WD Proxy] </TD></TR>
[WD Proxy] <TR><TD>
[WD Proxy] <FONT face="Helvetica">
[WD Proxy] This is typically caused by an incorrect username and/or password, but could also be caused by network problems.
[WD Proxy] </FONT>
[WD Proxy] </TD></TR>
[WD Proxy] <TR><TD>
[WD Proxy] <FONT face="Helvetica" SIZE=2>
[WD Proxy] <BR>
[WD Proxy]
[WD Proxy] </FONT>
[WD Proxy] </TD></TR>
[WD Proxy] </TABLE>
[WD Proxy] </blockquote>
[WD Proxy] </FONT>
[WD Proxy] </BODY></HTML>
[WD Proxy]
```

You need to allow Appium a no proxy connection to localhost to communicate with the device. To do that, simply add _`no_proxy=localhost`_ environment variable like this:

| Windows                  | Mac / Linux                 |
| ------------------------ | --------------------------- |
| `set no_proxy=localhost` | `export no_proxy=localhost` |

You can add it for the CLI session, or at the system level from the environment variables page on Windows/Mac.
