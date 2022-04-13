---
description: Testing without cables
---

# How to connect an Android device via WiFi

In this article, you will learn how to connect the Android device to your TestProject account and run test recording and execution via WiFi.

## Requirements for connection  <a href="#requirements-for-connection" id="requirements-for-connection"></a>

One-time device connection via USB.\
Android ADB (platform-tools) _\[Official link to get the platform-tools_ [_HERE_](https://developer.android.com/studio/releases/platform-tools)_]_\
Installed and running TestProject agent _\[Agent download page link_ [_HERE_](https://app.testproject.io/#/download)_]_

## Connection Guide <a href="#connection-guide" id="connection-guide"></a>

1. Connect your device to the computer
2. Open a platform-tools folder and copy its path

![](<../../.gitbook/assets/image (532).png>)

\
&#x20; 2\. Open a command prompt and navigate the platform-tools folder\
cd C:\Program Files\TestProject Agent\android-sdk\platform-tools\


![](<../../.gitbook/assets/image (465).png>)

3\. Run the next commands in the command prompt (one after another, not all at once)\
adb tcpip 5555\
adb shell "ip addr show wlan0 | grep -e wlan0$ | cut -d\\" \\" -f 6 | cut -d/ -f 1"\
After the second command, you will have the IP address of your Android device\
\


![](<../../.gitbook/assets/image (541).png>)

\
Type the next command in the command prompt\
adb connect _ip\_address_:5555\
Where _ip\_address_ is the IP of your mobile phone.

![](<../../.gitbook/assets/image (558).png>)

Now you can disconnect your device from the cable, and the device is connected via WiFi :)

