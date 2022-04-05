---
description: >-
  In this article I will explain how to run the agent on Linux distro CentOS
  version 6
---

# Launching the TestProject agent on CentOS 6

Since CentOS 6 has older version of libc++ and glib libraries, and those can not be updated without breaking the OS, the agent can not be run from it's native launcher.

Therefore only Web and Android tests can be executed, since ios-tools require those libraries.

### How to run the agent <a href="#how-to-run-the-agent" id="how-to-run-the-agent"></a>

1. Open the terminal and cd to \~/testproject/agent
2. run the following code&#x20;

```
nohup ./jre/bin/java -jar io.testproject.agent.launcher.jar &
```

After that, the agent will start and you can close the terminal.\
\
**Important**: CentOS 6 does NOT support chrome browser, therefore you can **NOT** record test, but you can execute any Android and Web test ( Not on Chrome) , as well as coded tests of course.

Happy testing!
