---
description: Here we will go over the common registration issues with their solutions.
---

# Can't register your agent?

In this article we will troubleshoot some common agent registration issues.\
In case you have not succeeded in registering your agent, as explained [here](https://docs.testproject.io/getting-started/installation-and-setup), this article will help you resolve your issue.\


## Windows <a href="#windows" id="windows"></a>

**Move agent from one account to the other:**\
\
Let's say you need to move your agent to a different account, maybe because you were invited to a new team. Open windows files explorer and navigate to `%appdata%`\
Then open the TestProject Agent folder and delete the file named `agentIdentity.jbin` or the file named id.dat (only one of them will most likely show, if both, delete both of them). Reset your agent. Now try to register your agent as shown below.

**Having trouble registering the agent:**

If you have downloaded the agent and have trouble registering it, a few options might help while trying them. Each time try to register the agent like so:

Go to agents and click register. A message will pop up and ask you to input the agent's alias, so just type in the name you want.

![](https://downloads.intercomcdn.com/i/o/200713982/17e80e27ba6641633ca13f2e/image.png)

After registration is complete, you should see the "TV" icon go green, and your agent with the name you gave it pop up under My Agents.

![](https://downloads.intercomcdn.com/i/o/200713248/2812dd6b9f86d6bfca1b5048/image.png)

1. Make sure the agent is running,

( to check this, click the icon shown below, it will show the status of the agent)

![](https://downloads.intercomcdn.com/i/o/199644283/0552473a2b5d1ae4c511f172/image.png)

_**2.**_ If the agent is running and you are getting an "unable to register" error, go to the agent's installation folder. On windows, the agent is typically located in C:\Program Files\TestProject Agent\
Delete data.bin in the agent folder (only if it is there)\
And now just run the executable&#x20;

![](https://downloads.intercomcdn.com/i/o/199628206/94cd5f15cc6a7dc6cdf18092/image.png)

\
\
**3.** _click the icon-_

![](https://downloads.intercomcdn.com/i/o/199644283/0552473a2b5d1ae4c511f172/image.png)

Then click restart.\
\
**4.** _Restart your system._

&#x20;_**5.**_ Reinstall the agent. To do that, click the uninstall.exe in the agent's folder, then open windows files explorer and navigate to `%appdata%`, go to TestProject folder, and delete the folder named Agent. Now reinstall the agent.

If all those steps fail, contact support.\
\


## MacOS <a href="#macos" id="macos"></a>

**Registering the agent:**\
On Mac, after installing the agent, you can run it by finding it in the application folder and double-clicking. This will open it in the dock, and you can see its options by right-clicking.&#x20;

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/200730456/843f773ff80efc6a8ebb55e4/assets-2F-Ll7jrseWgVXoVhnULBe-2F-Lo0Ug96w5K3B7yLMRwX-2F-Lo0aajB-Z-QY-cPuv4l-2Fimage.png)

Then when you run it, you will have the TestProject icon on the top taskbar, with the same options as in windows.\


![](https://downloads.intercomcdn.com/i/o/200721198/62c921b1dcb902c991e5a6ee/Screen+Shot+2020-04-15+at+10.44.46+AM111.png)

Click it and make sure it says "Running".\
Now try registering your agent like on the windows steps (all troubleshooting steps but steps 2 and 5 apply, the folder for step 5 on mac is the one shown below in moving the agent between accounts). If that does not work, then contact support.

**Move agent from one account to the other:**

On MacOS, you need to go to your user's folder and enable "view libraries", so right-click and click "Show View Options":

![](https://downloads.intercomcdn.com/i/o/200728709/946219db9dfcac5799d03f82/Screen+Shot+2020-04-15+at+10.44.46+AM.png)

then enable "Show Library Folder":

![](https://downloads.intercomcdn.com/i/o/200729223/5f9e4fbb64cc29d981847c81/Screen+Shot+2020-04-15+at+10.44.55+AM.png)

Now go to Library>Application Support>TestProject>Agent\
and delete agentidentity.jbin or id.dat.

![](https://downloads.intercomcdn.com/i/o/200729505/c0a4291399ab6e415a98630a/Screen+Shot+2020-04-15+at+10.45.05+AM.png)

![](https://downloads.intercomcdn.com/i/o/200729527/c65edcbab7e6b2069ceabc0f/Screen+Shot+2020-04-15+at+10.45.36+AM.png)

Now you can register your agent.\
If that does not work, delete the entire Agent folder, reinstall the agent and try again.

### Linux/Ubuntu <a href="#linuxubuntu" id="linuxubuntu"></a>

**Registering the agent:**

On Linux, you will need to run the `TestProjectAgent` command from the `testproject/agent` folder

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/200736772/b9a99b0bdf003fb9faf6806f/assets-2F-Ll7jrseWgVXoVhnULBe-2F-LmumzLMfJDGvW7Gnxps-2F-Lmun9lMYfn8qn5QlyCh-2Fimage.png)

Now troubleshoot using the windows steps, except steps 2 and 5. the folder for step 5 on Linux is: \~/.testproject/agent.

### Important! <a href="#important" id="important"></a>

Before re-installing the Agent on Linux, make sure you delete the **.TestProject hidden directory.**

Run the command: ls -a to verify the directory is there.

After deleting it, you may install the Agent again.

**Move agent from one account to the other:**\
navigate to \~/.testproject/agent, and delete agentidentity.jbin or id.dat.\
then re-register your agent.\
\
If all of the above fails, contact support.
