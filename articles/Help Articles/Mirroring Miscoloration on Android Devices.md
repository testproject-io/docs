---
description: >-
  Steps that need to be taken in case of miscoloration during Android device
  mirroring.
---

# Mirroring Miscoloration on Android Devices

In case you are experiencing miscoloration while mirroring your Android device on TestProject during **recording or mirroring**, such as in the following example:

![](<../../.gitbook/assets/image (536) (1) (1).png>)

Please follow the steps below.

This tutorial is intended for Android devices that are being used on TestProject through **Chromium based browsers** such as **Google Chrome** or **Microsoft Edge** (Also known as Chromium Edge).

1. Navigate to: **chrome://flags/#force-color-profile** or **edge://flags/#force-color-profile** based on your browser.

You will see the following page:

![](<../../.gitbook/assets/image (471) (1).png>)

2\. Select the **scRGB liner** option from the dropdown list and **relaunch the browser**:

![](<../../.gitbook/assets/image (469) (1) (1).png>)

![](<../../.gitbook/assets/image (564).png>)

Afterward, attempt to mirror your device again.

3\. **(Optional)** In case the above option did not resolve the issue, select **HDR10** and try again:\


![](<../../.gitbook/assets/image (454) (1).png>)
