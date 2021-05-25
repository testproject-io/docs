---
description: Unregistered or Disconnected Agent
---

# Unregistered/Offline Agent

TestProject Agent uses the TestProject cloud in oder to operate. Trough this communication channel, it can download an up-to-date dependencies, such as the Web or Mobile drivers or other components needed to operate correctly.

### Unregistered Agent and Offline Mode

When the Agent is not registered and not authenticated with your TestProject account, it can still operate  using the components that were bundled into the installer. However this implies several limitations, for example a version mismatch might occur, between the installed browser or the connected device and the bundled driver version.

Same limitations apply to a scenario when the Agent is offline and is not able to communicate with the TestProject cloud \(even after it has been successfully registered\). Not being able to update the drivers and other component to match the version of the installed browsers or the connected devices, won't allow the TestProject Agent functioning correctly and will lead to:

* Failure to open a recording session
* Failure to mirror devices
* Failure to execute tests or job
* Failure to open a Development session using the SDKs

These errors will be clearly outlined in one of the following:

* Popup presented in the browser
* SDK console logs
* Execution reports

The best solution in order to resolve this situation is to ensure that:

* TestProject Agent is registered
* TestProject Agent can connect to the internet
* TestProject Agent is not restricted from communicating with the TestProject cloud.

Common scenarios for communication failures might be:

* Firewall blocking any external communication with h_ttps://testproject.io_
* VPN routing the all traffic to an internal network and not to the internet \(outside world\).
* DNS settings are invalid or do not allow resolution of internet addresses.
* Antivirus or Security software communication.

### Manual Drivers Update

When resolving the issues above and ensuring a proper communication channel is not possible, there is a manual way for updating the web drivers used by the Agent to operate the web browsers.

Agent stores the drivers in:

* Windows - `%appdata%\TestProject\Agent\deps\drivers`
* MacOS - `~/Library/Application Support/TestProject/Agent/deps/drivers`
* Linux - `./testproject/agent/deps/drivers`
* Docker - `/var/testproject/agent/deps/drivers`

### Update Procedure

1. Download the relevant driver and place it in the right location.
   1. Chrome - [https://chromedriver.chromium.org/downloads](https://chromedriver.chromium.org/downloads)
   2. Firefox - [https://github.com/mozilla/geckodriver/releases](https://github.com/mozilla/geckodriver/releases)
   3. Chromium Edge - [https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver](https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver/)
2. Determine yo browser version:
   1. In Chrome open chrome://version/
   2. In Firefox, check in the about menu.
   3. In Chromium Edge open edge://settings/help
3. Create a "version" folder under the Browser folder with the exact version number
4. Extract the driver executable and place it into the version folder
5. Place the same executable in the `workdir` folder

![](../.gitbook/assets/image%20%2837%29.png)



