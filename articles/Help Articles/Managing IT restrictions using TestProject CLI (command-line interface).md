---
description: >-
  Blocked executables, CLI, starting the agent with a custom data folder, VPN
  settings, firewall, network issues, proxy issues, using TestProject CLI
  (command-line interface)
---

# Managing IT restrictions

### **TestProject Agent and Organization Security** <a href="#h_d572b3a01f" id="h_d572b3a01f"></a>

If you are trying to use the TestProject Agent in a restricted environment, with various security policies in place, that are blocking the Agent components from getting started, you might encounter errors.

#### Installation on a restricted file system <a href="#h_53532328e9" id="h_53532328e9"></a>

If you are experiencing errors when trying to install the TestProject Agent, you might need to install it into a special provisioned folder, authorized to deploy and run vendor executables.

In some cases, a temporary administrative privilege might be required - if this is the case please contact your IT department and file a request for the necessary access. Note that running the Agent is always possible with a standard user (without special or administrative privileges).

#### Running and Recording tests in a restricted environment <a href="#h_fc194222e7" id="h_fc194222e7"></a>

Some organizations only allow running executables on their computers from a special folder.

TestProject Agent depends on other executables like the browser drivers. If your IT restrictions prevent a program to launch other executables, please check with your IT department what is filesystem location you can use to launch executables freely.

Assuming we use the location `C:\sandbox` as an example for an unrestricted location. Let's create a `TestProject` folder inside and start the TestProject Agent using the CLI (via command-prompt or terminal) with this custom data path:

```shell
testproject-agent start --data-path=C:\sandbox\TestProject -f
```

#### Manual Drivers Updating <a href="#h_a46d586b1b" id="h_a46d586b1b"></a>

In case your Agent is not registered and is not able to get registered, you might need to update the drivers manually.

Refer to the following guide on how this should be done: [https://docs.testproject.io/testproject-agents/unregistered-offline-agent#manual-drivers-update](https://docs.testproject.io/testproject-agents/unregistered-offline-agent#manual-drivers-update)

If you are still getting errors and blockage notification for Java or other processes, make sure to allow them and allow the drivers to get launched, otherwise you might see errors during your attempts to record or execute tests.

### Network <a href="#h_49ee42ce54" id="h_49ee42ce54"></a>

When your organization prevents communication outside of the internal network, and your attempts to register an Agent fail, you will need to contact your IT department and allow:

* Communication with `*.testproject.io`&#x20;
* Communication with   `*.tpagent.io`
* Make sure the user account that runs the TestProject Agent has permissions for binding to ports `8585` and `8443` on localhost/127.0.0.1

If these ports are blocked for some reason you can change the default ports using the CLI as explained here: [https://docs.testproject.io/testproject-agents/testproject-agent-cli](https://docs.testproject.io/testproject-agents/testproject-agent-cli#start) in the `Start` command description, and the _external connectivity_ section using the `--rest-address` option.

Besides the ability to change the default listening port using the technique above, it is also possible to allow external access to the Agent, specifically for communicating with it over the internal network using other interfaces such as the SDK.

Refer to this blog post for more information:

[https://blog.testproject.io/2021/04/28/distributed-execution-for-test-automation/](https://blog.testproject.io/2021/04/28/distributed-execution-for-test-automation/)
