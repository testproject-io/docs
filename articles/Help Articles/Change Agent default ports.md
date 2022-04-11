---
description: >-
  This article describes how to change the default ports the agent binds to at
  start-up
---

# Change Agent default ports

Sometimes when using TestProject Agent you might encounter an issue where the Agent default ports are already in use by another program. It's also possible that in some organizations biding to localhost can only be done on specific ports.

In this article, we will explain how to check if another program is using the Agent ports and how to change the Agent default ports. So we can work in a restricted environment.

If you are running in a restricted environment that does not allow binding to ports 8585 / 8433 you can skip to part #2 - [change default ports](https://intercom.help/testprojectio/en/articles/5648808-change-agent-default-ports#h\_39d1403908)

### 1) Check if the ports are being used by another program <a href="#h_bb06812f4d" id="h_bb06812f4d"></a>

First, let's run a scan to check if there are other processes that are using the Agent default ports. For that, we will need to quit the TestProject Agent.

#### Windows: <a href="#h_0c42e1ebe1" id="h_0c42e1ebe1"></a>

Open PowerShell as an **admin** and then run the following command:

**`Get-Process -Id (Get-NetTCPConnection -LocalPort 8585).OwningProcess`**

**`Get-Process -Id (Get-NetTCPConnection -LocalPort 8443).OwningProcess`**

#### macOS / Ubuntu: <a href="#h_90339d6bd7" id="h_90339d6bd7"></a>

Open Terminal and then run the following command:

**`sudo lsof -i :8585`**

**`sudo lsof -i :8443`**

If anything uses these ports when the agent is turned off, that means we should change the Agent default ports.

### 2) Change default ports <a href="#h_39d1403908" id="h_39d1403908"></a>

You can change the agent default ports from here.

#### Windows: <a href="#h_65f13e6775" id="h_65f13e6775"></a>

navigate to `%appdata%/TestProject/Agent` in your run command (`⊞ WinKey + R`):

![](<../../.gitbook/assets/image (7) (1).png>)

you can change the ports from here:

![](<../../.gitbook/assets/image (8) (1).png>)

#### macOS: <a href="#h_6e4a920fb2" id="h_6e4a920fb2"></a>

﻿Open `Files Finder` and choose `Go` form the top menu, select `Go to Folder` and type:\
﻿ `~/Library/Application Support/TestProject/Agent/agent-configuration.json`

![](<../../.gitbook/assets/image (9) (1).png>)

**Linux**\
﻿Navigate to `~/.testproject/agent/` and edit the ports using the command:

`vi agent-configuration.json` from terminal or use any editing tool.

![](<../../.gitbook/assets/image (10) (1).png>)

_**Note:**_

You can change the proxy and bind the agent to a different interface (IP address) from the same config file.
