---
description: Here we'll explain how to change the agent's port.
---

# Can I change the agent's port?

In this article we'll go over how you can change the port your agent uses manually.\
Before starting, please note that this must be done only **after the agent is registered!**\
If you do this before registering the agent, the TestProject web application will not be able to link the agent to your account as it communicating with port 8585 explicitly.\
\
To change the port, go to your agent's folder located at:\
**%appdata%\TestProject\Agent**\
\
Locate the **agent-configuration.json** file and open it.\


![](<../../.gitbook/assets/image (533).png>)

\
Inside this file, you'll be able to edit the **bindPort** and/or **bindSecurePort** values to whatever you need.

![](<../../.gitbook/assets/image (509).png>)

\
**\*\*Important note:** Please be careful when editing the file, if the JSON file structure is harmed, the agent won't be able to launch!
