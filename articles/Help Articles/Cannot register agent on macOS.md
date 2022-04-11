---
description: Common macOS agent troubleshooting
---

# Cannot register agent on macOS

After downloading the agent, if you are having trouble registering it, follow the steps here.

In the agent's tab, to register an agent- click register. A message will pop up, and ask you to input the agent's alias, just type in the name you want.\
If you get an error, follow the steps below.

![](https://downloads.intercomcdn.com/i/o/200713982/17e80e27ba6641633ca13f2e/image.png)

After registration is complete (if you got no errors), you should see the "TV" icon go green, and your agent with the name you gave it pop up under My Agents.

![](https://downloads.intercomcdn.com/i/o/200713248/2812dd6b9f86d6bfca1b5048/image.png)

If you get a registration error:

1\. Make sure the agent is running. To check this, click the icon shown below; it will show the agent's status.

![](https://downloads.intercomcdn.com/i/o/200721198/62c921b1dcb902c991e5a6ee/Screen+Shot+2020-04-15+at+10.44.46+AM111.png)

If the status is not "Running," click restart and check again. If it is running, try registering again. If that failed, repeat the step with a computer restart. If that also failed, go to step 2.

_**2.**_ Reinstall the agent. To do that on MacOS, you need to first go to your user's folder and enable "view libraries", so right-click and click "Show View Options":

![](https://downloads.intercomcdn.com/i/o/200728709/946219db9dfcac5799d03f82/Screen+Shot+2020-04-15+at+10.44.46+AM.png)

then enable "Show Library Folder":

![](https://downloads.intercomcdn.com/i/o/200729223/5f9e4fbb64cc29d981847c81/Screen+Shot+2020-04-15+at+10.44.55+AM.png)

![](https://downloads.intercomcdn.com/i/o/200729505/c0a4291399ab6e415a98630a/Screen+Shot+2020-04-15+at+10.45.05+AM.png)

Now go to Library>Application Support>TestProject\
and delete the folder named "Agent", then re-install the agent (do not forget to make sure it is running as shown in step 1).\
Now you can register your agent.\
If all those steps fail, contact support.
