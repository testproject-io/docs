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

![](<../../.gitbook/assets/image (471).png>)

After registration is complete, you should see the "TV" icon go green, and your agent with the name you gave it pop up under My Agents.

![](<../../.gitbook/assets/image (518).png>)

1. Make sure the agent is running,

( to check this, click the icon shown below, it will show the status of the agent)

![](<../../.gitbook/assets/image (543).png>)

_**2.**_ If the agent is running and you are getting an "unable to register" error, go to the agent's installation folder. On windows, the agent is typically located in C:\Program Files\TestProject Agent\
Delete data.bin in the agent folder (only if it is there)\
And now just run the executable&#x20;

![](<../../.gitbook/assets/image (458).png>)

\
\
**3.** _click the icon-_

![](<../../.gitbook/assets/image (506).png>)

Then click restart.\
\
**4.** _Restart your system._

&#x20;_**5.**_ Reinstall the agent. To do that, click the uninstall.exe in the agent's folder, then open windows files explorer and navigate to `%appdata%`, go to TestProject folder, and delete the folder named Agent. Now reinstall the agent.

If all those steps fail, contact support.\
\


## MacOS <a href="#macos" id="macos"></a>

**Registering the agent:**\
On Mac, after installing the agent, you can run it by finding it in the application folder and double-clicking. This will open it in the dock, and you can see its options by right-clicking.&#x20;

![](<../../.gitbook/assets/image (460).png>)

Then when you run it, you will have the TestProject icon on the top taskbar, with the same options as in windows.\


![](<../../.gitbook/assets/image (534).png>)

Click it and make sure it says "Running".\
Now try registering your agent like on the windows steps (all troubleshooting steps but steps 2 and 5 apply, the folder for step 5 on mac is the one shown below in moving the agent between accounts). If that does not work, then contact support.

**Move agent from one account to the other:**

On MacOS, you need to go to your user's folder and enable "view libraries", so right-click and click "Show View Options":

![](<../../.gitbook/assets/image (486) (1).png>)

then enable "Show Library Folder":

![](<../../.gitbook/assets/image (478).png>)

Now go to Library>Application Support>TestProject>Agent\
and delete agentidentity.jbin or id.dat.

![](<../../.gitbook/assets/image (509) (1).png>)

![](<../../.gitbook/assets/image (463).png>)

Now you can register your agent.\
If that does not work, delete the entire Agent folder, reinstall the agent and try again.

### Linux/Ubuntu <a href="#linuxubuntu" id="linuxubuntu"></a>

**Registering the agent:**

On Linux, you will need to run the `TestProjectAgent` command from the `testproject/agent` folder

![](<../../.gitbook/assets/image (539).png>)

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
