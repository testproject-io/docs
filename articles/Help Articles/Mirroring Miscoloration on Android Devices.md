---
description: >-
  Steps that need to be taken in case of miscoloration during Android device
  mirroring.
---

# Mirroring Miscoloration on Android Devices

In case you are experiencing miscoloration while mirroring your Android device on TestProject during **recording or mirroring**, such as in the following example:

![](https://downloads.intercomcdn.com/i/o/250590743/6f677a3db4f5e9eaaa334301/image.png)

Please follow the steps below.

This tutorial is intended for Android devices that are being used on TestProject through **Chromium based browsers** such as **Google Chrome** or **Microsoft Edge** (Also known as Chromium Edge).

1. Navigate to: **chrome://flags/#force-color-profile** or **edge://flags/#force-color-profile** based on your browser.

You will see the following page:

![](https://downloads.intercomcdn.com/i/o/250653493/d03912066d885d4a943b11f6/image.png)

2\. Select the **scRGB liner** option from the dropdown list and **relaunch the browser**:

![](https://downloads.intercomcdn.com/i/o/250655701/bca41df5a0955290dc7587f4/image.png)

![](https://downloads.intercomcdn.com/i/o/250656234/bca262389b45c7244096b869/image.png)

Afterwards, attempt to mirror your device again.

3\. **(Optional)** In case above option did not resolve the issue, select **HDR10** and try again:\


![](https://downloads.intercomcdn.com/i/o/250655911/af332244d3aa9d655640b472/image.png)
