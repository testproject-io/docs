---
description: UIAutomator - Power Consumption
---

# UIAutomator - Power Consumption

In case you are running a Android device and having issues with UIAutomator.\
You need to make sure that the Appium, UIAutomator, the Application Under Test and other related automation tools, are not power restricted.

Here is a list containing the apps that you should **disable** optimization on.

#### Applications list: <a href="#h_8c1e16a665" id="h_8c1e16a665"></a>

* **AUT** (Application under test / Your application)
* Android System WebView (for applications using WebView)
* Appium Settings
* Application Installer
* Automation Test
* Chrome (for web tests on mobile)
* **io.appium.uiautomator2.server**
* **io.appium.uiautomator2.server.test**

To achieve that do the following:

#### **Vivo devices**: <a href="#h_5f4822842d" id="h_5f4822842d"></a>

For Vivo devices you can follow the official documentation [here](https://www.vivo.com/en/support/questionList?categoryId=10054).

#### Samsung devices: <a href="#samsung-devices" id="samsung-devices"></a>

* Access Battery settings > App Power Saving > Details >  [Applications list](<UIAutomator - Power Consumption.md>) to disable > Disabled

**On New Samsung Devices:**

* Settings > Apps > Context Menu >  Special Access > Optimise battery usage > Apps not optimised -> Show all -> Disable [Applications list](<UIAutomator - Power Consumption.md>)
* Settings > Device Care > Battery > High Performance

#### Huawei devices: <a href="#huawei-devices" id="huawei-devices"></a>

* Turn Energy Settings to Normal and add  **Applications list** to **Protected Apps.**

#### HTC devices: <a href="#htc-devices" id="htc-devices"></a>

* Phone Settings -> Battery -> Power Saving Mode -> Battery Optimization -> select [Application list](<UIAutomator - Power Consumption.md>) -> don’t optimise -> save.

#### Google Devices: <a href="#google-devices" id="google-devices"></a>

* Settings > Battery Saver > Off
* Settings > Apps & Notifications > Special app access > Battery optimisations > Not Optimised ([Application list](<UIAutomator - Power Consumption.md>) should be in this section )
* Settings > Apps & Notifications > App Info >  [Application list](<UIAutomator - Power Consumption.md>) > Advanced (Battery) > Background Restriction = Background usage can't be restricted.
* Settings > Apps & Notifications > App Info >  [Application list](<UIAutomator - Power Consumption.md>) > Advanced (Battery) > Battery Optimisation = Not Optimised

#### Google Devices and Android 10: <a href="#google-devices-and-android-10" id="google-devices-and-android-10"></a>

Open Settings on your device then check the following:

* Battery > Battery Saver > Off
* Apps & Notifications (Press see all apps) >  [Application list](<UIAutomator - Power Consumption.md>) > Battery > Battery Optimisation > (Should be **Not** optimised)
