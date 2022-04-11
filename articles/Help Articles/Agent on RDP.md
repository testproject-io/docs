# Agent on RDP

Only a single Agent instance can run on a machine, even on a server that allows multiple RDP connections. When a test is running, the browser process is spawned under the same session where the user started the Agent (e.g. session #1). When another user in another session (e.g. session #2) starts a test, it will run in the first session, and the user won't see it.

This behavior is normal.

For recording and debugging purposes, you should install an Agent on your physical computer. You can use the server for headless (aka lab) executions.
