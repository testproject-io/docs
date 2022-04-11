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

![](https://downloads.intercomcdn.com/i/o/178893053/be2704ab77e13047d93ca24d/2020-01-22\_18h31\_02.png)

\
&#x20; 2\. Open a command prompt and navigate the platform-tools folder\
cd C:\Program Files\TestProject Agent\android-sdk\platform-tools\


![](https://downloads.intercomcdn.com/i/o/178893565/8150ab5a0828f7743e9b0f16/2020-01-22\_18h32\_57.png)

3\. Run the next commands in the command prompt (one after another, not all at once)\
adb tcpip 5555\
adb shell "ip addr show wlan0 | grep -e wlan0$ | cut -d\\" \\" -f 6 | cut -d/ -f 1"\
After the second command, you will have the IP address of your Android device\
\


![](https://downloads.intercomcdn.com/i/o/178897321/4932fd008a6e192fb1f6f915/2020-01-22\_18h42\_48.png)

\
Type the next command in the command prompt\
adb connect _ip\_address_:5555\
Where _ip\_address_ is the IP of your mobile phone.

![](https://downloads.intercomcdn.com/i/o/178903036/f7e3f50a95b7c63f9ad2a954/2020-01-22\_18h58\_36.png)

Now you can disconnect your device from the cable, and the device is connected via WiFi :)

![](https://downloads.intercomcdn.com/i/o/178903271/6fe9cab3eba202609c7f94db/2020-01-22\_18h59\_18.png)
