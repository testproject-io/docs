---
description: >-
  First steps to start recording and executing mobile tests on Android Emulators
  using Android Studio
---

# Start Android Emulator using Android studio

Sometimes you want to record and execute tests on a device that is physically not available to you, that is why in TestProject you can use Emulators.

This is how you start an emulator from Android Studio:

First, you install android studio from here: [https://developer.android.com/studio](https://developer.android.com/studio)

After installation you go to tools-> AVD Manager:

\
﻿Then you do the following:

![](<../../.gitbook/assets/image (462) (2).png>)

Select the device you wish to emulate then select the version, after that you can fine tune it to your desires or just open the emulator and start testing.

![](../../.gitbook/assets/Emulator.gif)

#### Common Issues: <a href="#h_b16066b03f" id="h_b16066b03f"></a>

1\) If the agent does not recognize the emulator after installation, please restart your agent.

2\) If you do not see the device on TestProject please set the following option on the Emulator and restart it:

![](<../../.gitbook/assets/image (453) (2).png>)
