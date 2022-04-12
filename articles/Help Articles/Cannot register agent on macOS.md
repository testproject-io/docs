---
description: Common macOS agent troubleshooting
---

# Cannot register agent on macOS

After downloading the agent, if you are having trouble registering it, follow the steps here.

In the agent's tab, to register an agent- click register. A message will pop up, and ask you to input the agent's alias, just type in the name you want.\
If you get an error, follow the steps below.

![](<../../.gitbook/assets/image (548).png>)

After registration is complete (if you got no errors), you should see the "TV" icon go green, and your agent with the name you gave it pop up under My Agents.

![](<../../.gitbook/assets/image (517) (1).png>)

If you get a registration error:

1\. Make sure the agent is running. To check this, click the icon shown below; it will show the agent's status.

![](<../../.gitbook/assets/image (525).png>)

If the status is not "Running," click restart and check again. If it is running, try registering again. If that failed, repeat the step with a computer restart. If that also failed, go to step 2.

_**2.**_ Reinstall the agent. To do that on MacOS, you need to first go to your user's folder and enable "view libraries", so right-click and click "Show View Options":

![](<../../.gitbook/assets/image (496).png>)

then enable "Show Library Folder":

![](<../../.gitbook/assets/image (467).png>)

![](<../../.gitbook/assets/image (459) (1).png>)

Now go to Library>Application Support>TestProject\
and delete the folder named "Agent", then re-install the agent (do not forget to make sure it is running as shown in step 1).\
Now you can register your agent.\
If all those steps fail, contact support.
