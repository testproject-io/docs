---
description: This article will show you how to enable IOS simulators and fix common issues
---

# Using IOS Simulators with TestProject using XCode

The simulator app, available within Xcode, presents the iPhone or iPad user interface in a window on your Mac computer.

`It is not possible to run Xcode on a Windows or Linux operating systems.`

![](<../../.gitbook/assets/image (537).png>)

You interact with the Simulator by using the keyboard and the mouse to emulate taps, device rotation, and other user actions. It also allows you to automate your App without the need for a physical device.

### **Prerequisites** <a href="#h_45db5e0b06" id="h_45db5e0b06"></a>

* You need a Mac computer and macOS operating system.
* You need the TestProject Agent to be [installed ](https://docs.testproject.io/getting-started/installation-and-setup)and running on your computer.
* You need Xcode to be installed from [Mac App Store.](https://apps.apple.com/us/app/xcode/id497799835?ls=1\&mt=12)

### **Usage** <a href="#h_916ab6c175" id="h_916ab6c175"></a>

With Xcode installed:

![](<../../.gitbook/assets/image (489).png>)

The TestProject Agent will detect all the simulators it comes with and display them in the connected simulators list in the TestProject application:

![](<../../.gitbook/assets/image (474).png>)

If the simulators are still not detected even when Xcode is correctly installed, open the terminal (using Launchpad), and make sure you have an active developer directory by running the command below:

```
xcode-select -p
```

If you do not have such a directory, you'll see the following message:

```
xcode-select: error: unable to get active developer directory, use `sudo xcode-select --switch path/to/Xcode.app` to set one (or see `man xcode-select`)
```

You can then proceed to use the following command, and then restart the agent to detect the simulators:

```
sudo xcode-select --switch path/to/Xcode.app
```

You can mirror any iOS simulator screen:

![](<../../.gitbook/assets/image (521).png>)

There is no need to have an Apple Developer Account in order to do this (on the contrary to IOS physical devices).

Simulators are launched headless, but you can also start it from Xcode and see it's window mirrored in TestProject application.

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/291647782/20bc23cb37b55499d194deb6/assets-2F-Ll7jrseWgVXoVhnULBe-2F-MNAE-NrKn1uqd1F-DVn-2F-MNAVW9wYFHq-EJOoPrl-2FSide\_by\_Side.png)

### Common Issues: <a href="#h_463cb46ff8" id="h_463cb46ff8"></a>

#### Simulators not detected <a href="#h_e6e423518a" id="h_e6e423518a"></a>

_If the simulators are still not detected, try running the following command and then restart the agent:_

sudo xcode-select -s $(ls -td /Applications/Xcode\* | head -1)/Contents/Developer

#### WDA Errors: <a href="#h_273f60998a" id="h_273f60998a"></a>

If you encounter errors when starting WDA on your simulators that are similar to this:

```
2021-07-18 02:22:22.461 ERROR 37497 qtp499764573-13 i.t.a.i.n Failed trying to start WDA on 2D3C1771-938B-43D7-A95C-5CCB834CE63E for unknown reason java.util.concurrent.ExecutionException: java.io.IOException: There was a problem connecting to the simulator with the udid of 2D3C1771-938B-43D7-A95C-5CCB834CE63E
```

Try to run the following command to shutdown all XCode simulators running on the machine:

```
sudo xcrun simctl shutdown all
```

Then try to run your test again TestProject agent should automatically start the simulator.

\
