---
description: Enable USB Debugging, connect your physical Android device to the Agent
---

# Connect Android Device to TestProject

In order to Test physical Android device using TestProject agent you need to enable USB-Debugging and few other settings.

To enable USB Debugging please make sure all the settings on the device are exactly like this:

Enable "Developer options".\
﻿This could be done by entering "Settings" -> "About Phone" -> repeatedly tapping the "Build number".\
﻿You should get a message that says your enabled developer options.\
​

Inside "**Developer options**", enable:

* "Stay Awake",
* "**USB debugging**",
* "Disable Permissions Monitoring" option **if it's available**.
* Under "Select USB configuration" select "**MTP**" or "**File transfer**".
* Scroll down and turn the animation off for: "Window animation scale", "Transition animation scale", "Animator duration scale".

When you plug the USB cable to your Android device, you will be asked 2 things:

* Allow access to device data -> select "**YES**"
* Allow USB debugging -> select "**OK**"

Some devices require extra permissions try to follow these guides if you encounter an issue.

1. [Huawei Extra permissions](https://intercom.help/testprojectio/en/articles/3988423-huawei-devices-extra-permissions-required)
2. [realMe Extra permissions](https://intercom.help/testprojectio/en/articles/3777631-realme-devices-extra-permissions-required)
